---
title: 设置准确的命令 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET EXACT command [ODBC]
ms.assetid: 9533d3e0-e7c1-49de-a3a3-0cc4373a91cb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 686ecc89f44bac4b219b760e55160f451a15c503
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67997724"
---
# <a name="set-exact-command"></a>SET EXACT 命令
指定用于比较不同长度的两个字符串的规则。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 指定表达式必须匹配字符以使字符等效。 将忽略表达式中的任何尾随空格进行比较。 对于比较而言，这两个表达式中较短的一个用空白填充，以匹配较长的表达式的长度。  
  
 OFF  
 （默认值。）指定为等效，表达式必须与字符的字符匹配，直到到达右侧表达式的末尾。  
  
## <a name="remarks"></a>备注  
 如果两个字符串的长度相同，则 "设置确切" 设置不起作用。  
  
## <a name="string-comparisons"></a>字符串比较  
 Visual FoxPro 具有两个用于测试相等性的关系运算符。  
  
 = 运算符在同一类型的两个值之间执行比较。 此运算符适用于比较字符、数字、日期和逻辑数据。  
  
 但是，在将字符表达式与 = 运算符进行比较时，结果可能会与预期结果不完全相同。 字符表达式从左到右比较字符，直到其中一个表达式与另一个表达式不相等，直到达到 = 运算符右侧的表达式的末尾（设置为 "完全关闭"），或直到两个表达式的末尾都为已达到（精确设置）。  
  
 当需要精确比较字符数据时，可以使用 = = 运算符。 如果两个字符表达式与 = = 运算符进行比较，则 = = 运算符两侧的表达式必须包含完全相同的字符（包括空格）才能视为相等。 当使用 = = 比较字符串时，将忽略设置的确切设置。  
  
 下表显示了如何选择运算符和设置的确切设置如何影响比较。 （下划线表示空白空间。）  
  
|比较|= 精确|= 精确为|= = 完全打开或关闭|  
|----------------|------------------|-----------------|--------------------------|  
|"abc" = "abc"|匹配|匹配|匹配|  
|"ab" = "abc"|无匹配项|无匹配项|无匹配项|  
|"abc" = "ab"|匹配|无匹配项|无匹配项|  
|"abc" = "ab_"|无匹配项|无匹配项|无匹配项|  
|"ab" = "ab_"|无匹配项|匹配|无匹配项|  
|"ab_" = "ab"|匹配|匹配|无匹配项|  
|"" = "ab"|无匹配项|无匹配项|无匹配项|  
|"ab" = ""|匹配|无匹配项|无匹配项|  
|"__" = ""|匹配|匹配|无匹配项|  
|"" = "___"|无匹配项|匹配|无匹配项|  
|TRIM （"___"） = ""|匹配|匹配|匹配|  
|"" = TRIM （"___"）|匹配|匹配|匹配|  
  
## <a name="see-also"></a>另请参阅  
 [SET ANSI 命令](../../odbc/microsoft/set-ansi-command.md)
