---
title: 记录计数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- record count [ODBC]
- descriptors [ODBC], record count
ms.assetid: 46eec3cc-0ecc-4980-9020-fb74a9af5730
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4d684fb6d9614defdca3897c53c4bae9fc231a9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138075"
---
# <a name="record-count"></a>记录计数
描述符的 SQL_DESC_COUNT 标头字段是包含数据的编号最高的记录的从1开始的索引。 此字段不是所有列或绑定的参数的计数。 分配描述符时，SQL_DESC_COUNT 的初始值为0。  
  
 驱动程序采取任何必要的操作来分配和维护保存说明符信息所需的任何存储。 应用程序不会显式指定描述符的大小，也不会分配新记录。 当应用程序为其数字大于 SQL_DESC_COUNT 的值的描述符记录提供信息时，驱动程序将自动增加 SQL_DESC_COUNT。 当应用程序解除编号最高的描述符记录的绑定时，驱动程序将自动减小 SQL_DESC_COUNT 以包含剩余的最大记录数。
