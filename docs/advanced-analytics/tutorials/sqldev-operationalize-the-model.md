---
title: R + T-SQL 教程：运行预测
description: 教程演示如何使用 T-SQL 函数在 SQL Server 存储过程中操作嵌入式 R 脚本
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4b8e516d2e96c1cc4812a36800fd22371729445d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "73724865"
---
# <a name="lesson-4-run-predictions-using-r-embedded-in-a-stored-procedure"></a>第 4 课：使用嵌入到存储过程中的 R 来运行预测
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文属于有关如何在 SQL Server 中使用 R 的 SQL 开发者教程。

在此步骤中，你将了解如何针对新的观测值使用模型来预测潜在结果。 模型包装在存储过程中，该存储过程可由其他应用程序直接调用。 本演练演示了以下几种执行评分的方法：

- 批处理评分模式  ：使用 SELECT 查询作为存储过程的输入。 存储过程将返回与输入事例对应的观测表。

- 单独评分模式  ：传递一组单独的参数值作为输入。  存储过程将返回单个行或值。

首先，让我们看看一般情况下评分的工作原理。

## <a name="basic-scoring"></a>基本评分

存储过程 RxPredict 说明了在存储过程中包装 RevoScaleR rxPredict 调用的基本语法  。

```sql
CREATE PROCEDURE [dbo].[RxPredict] (@model varchar(250), @inquery nvarchar(max))
AS 
BEGIN 

DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);  
EXEC sp_execute_external_script @language = N'R',
  @script = N' 
    mod <- unserialize(as.raw(model)); 
    print(summary(mod)) 
    OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE); 
    str(OutputDataSet) 
    print(OutputDataSet) 
    ', 
  @input_data_1 = @inquery, 
  @params = N'@model varbinary(max)',
  @model = @lmodel2 
  WITH RESULT SETS ((Score float));
END
GO
```

+ SELECT 语句从数据库中获取序列化的模型，并将模型存储在 R 变量 `mod` 中以便使用 R 对其进行进一步处理。

+ 从 `@inquery` 中指定的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询中获得要评分的新案例，它是存储过程的第一个参数。 读取查询数据时，行保存在默认数据帧 `InputDataSet`中。 此数据帧将被传递给 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 中的 [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) 函数，该函数将生成评分。
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`
  
    由于数据帧可以包含单个行，你可以使用相同的代码来进行批量或单个评分。
  
+ `rxPredict` 函数返回的值是一个浮动值，该值表示司机获得小费（数量不限）的概率  。

## <a name="batch-scoring-a-list-of-predictions"></a>批处理评分（预测列表）

一种更常见的情况是在批处理模式下生成多个观察值的预测。 在此步骤中，让我们看看批处理评分的工作原理。

1.  先获取要处理的较小输入数据集。 此查询创建了“排名前 10”的行程列表，其中需要预测乘客计数和其他功能。
  
    ```sql
    SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance
    
    FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a

    LEFT OUTER JOIN

    (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052)    )b

    ON a.medallion=b.medallion AND a.hack_license=b.hack_license 
    AND a.pickup_datetime=b.pickup_datetime
    WHERE b.medallion IS NULL
    ```

    示例结果 
    
    ```sql
    passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime   direct_distance
    1  283 0.7 2013-03-27 14:54:50.000   0.5427964547
    1  289 0.7 2013-02-24 12:55:29.000   0.3797099614
    1  214 0.7 2013-06-26 13:28:10.000   0.6970098661
    ```

2. 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中创建名为 RxPredictBatchOutput 的存储过程  。

    ```sql
    CREATE PROCEDURE [dbo].[RxPredictBatchOutput] (@model varchar(250), @inquery nvarchar(max))
    AS
    BEGIN
    DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);
    EXEC sp_execute_external_script 
      @language = N'R',
      @script = N'
        mod <- unserialize(as.raw(model));
        print(summary(mod))
        OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);
        str(OutputDataSet)
        print(OutputDataSet)
      ',
      @input_data_1 = @inquery,
      @params = N'@model varbinary(max)',
      @model = @lmodel2
      WITH RESULT SETS ((Score float));
    END
    ```

3.  在变量中提供查询文本，并将其作为参数传递给存储过程：

    ```sql
    -- Define the input data
    DECLARE @query_string nvarchar(max)
    SET @query_string='SELECT TOP 10 a.passenger_count as passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance FROM  (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample  )a   LEFT OUTER JOIN (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052))b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'
    
    -- Call the stored procedure for scoring and pass the input data
    EXEC [dbo].[RxPredictBatchOutput] @model = 'RxTrainLogit_model', @inquery = @query_string;
    ```
  
存储过程将返回一系列值，表示对每个排名前 10 的行程的预测。 但是，排名靠前的行程也是单乘客行程，并且行程距离相对较短，司机不太可能获得小费。
  

> [!TIP]
> 
> 你可能还会返回该预测的概率评分（而不是返回“有小费”和“无小费”的结果），然后将 WHERE 子句应用到“分数”列的值以使用如 0.5 或 0.7 之类的阈值将评分分类为“可能会给小费”或“不可能给小费”  。 此步骤不包含在存储过程中，但很容易执行。

## <a name="single-row-scoring-of-multiple-inputs"></a>多个输入的单行评分

有时，你想要传入多个输入值，并基于这些值获取单个预测。 例如，你可以设置 Excel 工作表、Web 应用或 Reporting Services 报表，以调用存储过程和提供用户从这些应用程序中键入或选择的输入信息。

在本部分中，你将了解如何使用存储过程来创建单个预测，该存储过程采用多个输入（例如乘客计数、行程距离等）。 存储过程根据之前存储的 R 模型来创建分数。
  
如果从外部应用程序调用存储过程，请确保数据满足 R 模型的要求。 这可能包括确保输入的数据可以被转换为 R 数据类型或验证数据类型和数据长度。 

1. 创建存储过程 RxPredictSingleRow  。
  
    ```sql
    CREATE PROCEDURE [dbo].[RxPredictSingleRow] @model varchar(50), @passenger_count int = 0, @trip_distance float = 0, @trip_time_in_secs int = 0, @pickup_latitude float = 0, @pickup_longitude float = 0, @dropoff_latitude float = 0, @dropoff_longitude float = 0
    AS
    BEGIN
    DECLARE @inquery nvarchar(max) = N'SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs,  @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)';
    DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);
    EXEC sp_execute_external_script  
      @language = N'R',
      @script = N'  
        mod <- unserialize(as.raw(model));  
        print(summary(mod));  
        OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
        str(OutputDataSet);
        print(OutputDataSet); 
        ',  
      @input_data_1 = @inquery,  
      @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,@trip_time_in_secs int ,  @pickup_latitude float ,@pickup_longitude float ,@dropoff_latitude float ,@dropoff_longitude float', @model = @lmodel2, @passenger_count =@passenger_count, @trip_distance=@trip_distance, @trip_time_in_secs=@trip_time_in_secs, @pickup_latitude=@pickup_latitude, @pickup_longitude=@pickup_longitude, @dropoff_latitude=@dropoff_latitude, @dropoff_longitude=@dropoff_longitude  
      WITH RESULT SETS ((Score float));  
    END
    ```

2. 通过手动提供值来进行试用。
  
    打开一个新的“查询”窗口，调用存储过程，为每个参数提供值  。 参数表示模型所使用的功能列，并且这些参数是必需的。

    ```sql
    EXEC [dbo].[RxPredictSingleRow] @model = 'RxTrainLogit_model',
    @passenger_count = 1,
    @trip_distance = 2.5,
    @trip_time_in_secs = 631,
    @pickup_latitude = 40.763958,
    @pickup_longitude = -73.973373,
    @dropoff_latitude =  40.782139,
    @dropoff_longitude = -73.977303
    ```

    或者，使用[存储过程的参数](https://docs.microsoft.com/sql/relational-databases/stored-procedures/specify-parameters)支持的较短格式：
  
    ```sql
    EXEC [dbo].[RxPredictSingleRow] 'RxTrainLogit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

3. 结果表明从排名前 10 的行程中获得小费的概率非常低（零），因为所有这些行程都是距离相对较短的单乘客行程。

## <a name="conclusions"></a>结论

本步骤将结束教程。 至此，你已了解如何将 R 代码嵌入到存储过程，现在，你可以使用这些方法生成自己的模型。 与 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的集成使其更易于部署 R 模型以进行预测，将模型再定型合并为企业数据工作流的一部分也变得更加容易。

## <a name="previous-lesson"></a>上一课

[第 3 课：使用 T-SQL 定型和保存 R 模型](sqldev-train-and-save-a-model-using-t-sql.md)
