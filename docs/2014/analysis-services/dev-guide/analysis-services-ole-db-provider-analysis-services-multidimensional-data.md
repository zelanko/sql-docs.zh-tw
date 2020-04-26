---
title: Analysis Services OLE DB Provider （Analysis Services-多維度資料） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Analysis Services OLE DB Provider
ms.assetid: cdeecd50-1d91-4162-a4a2-01c7799b02a8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a0af68d7aa25d00f257399ade415e0287dd275fe
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "62732184"
---
# <a name="analysis-services-ole-db-provider-analysis-services---multidimensional-data"></a>Analysis Services OLE DB 提供者 (Analysis Services - 多維度資料)
  Analysis Services OLE DB Provider 是與[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]互動之應用程式的介面。 此介面會用於建立與多維度資料互動的用戶端應用程式。 這個提供者也提供方法，可針對多維度資料和關聯式資料進行線上和離線的資料採礦分析，而且會包含為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的一部分， 並且可由協力廠商用戶端應用程式轉散發。  
  
 Analysis Services OLE DB 提供者是與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 互動的主要方法，可用於完成與 Cube 或資料採礦模型連接、查詢 Cube 或資料採礦模型，以及擷取結構描述資訊等類工作。  
  
 做為獨立的提供者，Analysis Services OLE DB 提供者可為用戶端應用程式提供從關聯式和多維度來源建立本機 Cube 檔案和採礦模型的能力。 用戶端應用程式可以使用多維度運算式 (MDX) 來連接到本機 Cube 並執行查詢，而不必與執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的完整伺服器互動。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型資料存取 &#40;Analysis Services-多維度資料&#41;](../multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)  
  
  
