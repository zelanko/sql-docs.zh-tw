---
title: 管理快取 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- XMLA, cache
- XML for Analysis, cache
- clearing cache
- cache [Analysis Services]
ms.assetid: afad5c39-d4c3-4307-b3b9-a06617da0028
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7e99be9f6a2af7dbbaab624ba592b2486cf807f2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048158"
---
# <a name="managing-caches-xmla"></a>管理快取 (XMLA)
  您可以使用[ClearCache](../xmla/xml-elements-commands/clearcache-element-xmla.md) XML for Analysis (XMLA) 以清除指定的維度或是資料分割的快取中的命令。 清除快取會強制[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]重建該物件的快取。  
  
## <a name="specifying-objects"></a>指定物件  
 [物件](../xmla/xml-elements-properties/object-element-xmla.md)屬性`ClearCache`命令可以包含只針對下列物件的其中一個物件參考。 如果物件參考不是用於下列其中一個物件，就會發生錯誤：  
  
 [資料庫]  
 針對資料庫中包含的所有維度與資料分割清除快取。  
  
 維度  
 清除指定維度的快取。  
  
 Cube  
 針對 Cube 量值群組中包含的所有資料分割清除快取。  
  
 量值群組  
 針對量值群組中包含的所有資料分割清除快取。  
  
 資料分割  
 清除指定資料分割的快取。  
  
## <a name="see-also"></a>另請參閱  
 [在 Analysis Services 中使用 XMLA 進行開發](developing-with-xmla-in-analysis-services.md)  
  
  
