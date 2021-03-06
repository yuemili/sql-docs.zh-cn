---
title: 来自现有对象的数据源（数据源向导）（Analysis Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.datasourcewizard.specifyobject.f1
ms.assetid: e6ef6dea-9db8-45c4-8959-f9febd7caf7b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5576e997023e5a00cdecc3c2079ce387c7062ebb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66082380"
---
# <a name="data-sources-from-existing-objects-data-source-wizard-analysis-services"></a>来自现有对象的数据源（数据源向导）(Analysis Services)
  可以使用 **“来自现有对象的数据源”** 页，指定新数据源基于的现有数据源或项目。  
  
## <a name="options"></a>选项  
 **基于解决方案中的现有数据源创建数据源**  
 选择此选项可基于解决方案中的现有数据源创建新的数据源。 在生成、刷新或部署使用新数据源的项目时，新数据源将从您在选择此选项时指定的数据源获取设置。  
  
 **数据源**  
 从按项目分组的数据源列表中，选择希望新数据源基于的数据源。  
  
 **基于 Analysis Services 项目创建数据源**  
 选择此项可创建引用当前解决方案中另[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]一个项目的新数据源。 新数据源将从所选项目的 `TargetServer` 和 `TargetDatabase` 属性获取设置。 在生成、刷新或部署使用新数据源的项目时，新数据源将从您在选择此选项时指定的数据源获取设置。  
  
 **投影**  
 选择希望在新数据源中引用的项目。  
  
## <a name="see-also"></a>另请参阅  
 [数据源向导的 F1 帮助 &#40;Analysis Services&#41;](data-source-wizard-f1-help-analysis-services.md)   
 [多维模型中的数据源](multidimensional-models/data-sources-in-multidimensional-models.md)   
 [支持 &#40;SSAS 多维&#41;的数据源](multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  
