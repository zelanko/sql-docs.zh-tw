---
title: 管理快取（XMLA） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XMLA, cache
- XML for Analysis, cache
- clearing cache
- cache [Analysis Services]
ms.assetid: afad5c39-d4c3-4307-b3b9-a06617da0028
author: minewiskan
ms.author: owend
ms.openlocfilehash: cdc5bcd2e0500749edfa298a871b6fec7243ddfb
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544980"
---
# <a name="managing-caches-xmla"></a>管理快取 (XMLA)
  您可以使用 XML for Analysis （XMLA）中的[ClearCache](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/clearcache-element-xmla)命令，清除指定維度或資料分割的快取。 清除快取 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會強制重建該物件的快取。  
  
## <a name="specifying-objects"></a>指定物件  
 命令的[object](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)屬性只能 `ClearCache` 包含下列其中一個物件的物件參考。 如果物件參考不是用於下列其中一個物件，就會發生錯誤：  
  
 資料庫  
 針對資料庫中包含的所有維度與資料分割清除快取。  
  
 維度  
 清除指定維度的快取。  
  
 Cube  
 針對 Cube 量值群組中包含的所有資料分割清除快取。  
  
 量值群組  
 針對量值群組中包含的所有資料分割清除快取。  
  
 分割區  
 清除指定資料分割的快取。  
  
## <a name="see-also"></a>另請參閱  
 [在 Analysis Services 中使用 XMLA 進行開發](developing-with-xmla-in-analysis-services.md)  
  
  
