---
title: Analysis Services OLE DB 提供者 (Analysis Services-多維度資料) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Analysis Services OLE DB Provider
ms.assetid: cdeecd50-1d91-4162-a4a2-01c7799b02a8
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 32c717ef25e95192bceaa7084f3c8de63600f834
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133338"
---
# <a name="analysis-services-ole-db-provider-analysis-services---multidimensional-data"></a>Analysis Services OLE DB 提供者 (Analysis Services - 多維度資料)
  Analysis Services OLE DB 提供者是應用程式互動的介面[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 此介面會用於建立與多維度資料互動的用戶端應用程式。 這個提供者也提供方法，可針對多維度資料和關聯式資料進行線上和離線的資料採礦分析，而且會包含為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的一部分， 並且可由協力廠商用戶端應用程式轉散發。  
  
 Analysis Services OLE DB 提供者是與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 互動的主要方法，可用於完成與 Cube 或資料採礦模型連接、查詢 Cube 或資料採礦模型，以及擷取結構描述資訊等類工作。  
  
 做為獨立的提供者，Analysis Services OLE DB 提供者可為用戶端應用程式提供從關聯式和多維度來源建立本機 Cube 檔案和採礦模型的能力。 用戶端應用程式可以使用多維度運算式 (MDX) 來連接到本機 Cube 並執行查詢，而不必與執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的完整伺服器互動。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型資料存取&#40;Analysis Services-多維度資料&#41;](../multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)  
  
  