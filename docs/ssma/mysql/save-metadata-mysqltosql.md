---
title: 保存元数据（MySQLToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9bc6273f-e8b1-430b-81a5-14330a783562
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 549c4b88e7ca75ce86c8a4e2ddd3eba25f138583
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67929360"
---
# <a name="save-metadata--mysqltosql"></a>保存元数据 (MySQLToSQL)
保存**元数据**对话框会提示您在保存之前将元数据加载到 SSMA 项目中。 这样，你就可以拥有一个完整的项目文件，你可以脱机使用该文件并将其发送给其他人，例如技术支持人员。  
  
若要访问 "**保存元数据**" 对话框，请保存该项目。 如果缺少任何元数据，SSMA 将显示 "**保存元数据**" 对话框。  
  
## <a name="options"></a>选项  
**名称**  
项目中每个数据库的名称。  
  
**Status**  
指示元数据是否已加载到 SSMA 项目中，或元数据是否缺失。  
  
SSMA 根据需要将元数据加载到项目中。 浏览元数据和转换架构时，会自动加载元数据。  
  
**全选**  
选择所有列出的数据库。  
  
**清除**  
清除缺少元数据的所有数据库的复选框。 如果已加载元数据，则不能清除此复选框。  
  
**把**  
保存项目，为缺少元数据的所选数据库加载元数据。  
  
**取消**  
取消保存操作。 缺少元数据不会加载到项目中。  
  
