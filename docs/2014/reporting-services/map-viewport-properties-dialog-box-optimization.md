---
title: 地图视区属性对话框，优化 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.mapviewport.optimization.f1
- "10522"
ms.assetid: 8c0310ba-eedd-4c9f-95bd-1f9e2a1a8ed3
caps.latest.revision: 6
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: da12f40cba7da5a7c56d702c20d7ad2e7759b796
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37150248"
---
# <a name="map-viewport-properties-dialog-box-optimization"></a>“地图视区属性”对话框 -&gt;“优化”
  针对 **“地图视区属性”** 对话框选择 **“优化”** 有助于控制用于在报表中查看地图的分辨率。  
  
 当在报表中嵌入空间数据时，分辨率越高，则意味着要在报表中存储的数据越多。 当不在报表中嵌入空间数据时，分辨率越高，则意味着报表处理器要花越多的时间创建地图细节。 分辨率越低，意味着等待报表呈现的时间量越少。  
  
 单击 **“表达式”** (*fx*) 按钮以编辑设置该选项的值的表达式。  
  
## <a name="options"></a>“常规”  
 **“性能”**  
 滑动指针使之靠近 **“性能”** 可简化地图并减少其显示细节。  
  
 **质量**  
 滑动指针使之靠近 **“质量”** 将以较高的明细程度绘制地图。  
  
 **地图分辨率**  
 指定地图分辨率。 此值指定您要在呈现的地图中看到的最小明细程度（点数）。  
  
## <a name="see-also"></a>请参阅  
 [地图（报表生成器和 SSRS）](report-design/maps-report-builder-and-ssrs.md)   
 [报表故障排除： 地图报表&#40;报表生成器和 SSRS&#41;](report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md)  
  
  