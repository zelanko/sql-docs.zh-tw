---
title: "維度物件 (Analysis Services-多維度資料) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- dimensions [Analysis Services], objects
ms.assetid: 7f3d55c7-cccb-4ad0-b6cb-3a2c9992dd68
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 68fa5e37c0cc3620417f916ff35dcd6e3402d615
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="dimension-objects-analysis-services---multidimensional-data"></a>維度物件 (Analysis Services - 多維度資料)
  簡單 <xref:Microsoft.AnalysisServices.Dimension> 物件是由基本資訊、屬性和階層所組成。 基本資訊包括維度的名稱、維度的類型、資料來源、儲存模式等等。 屬性會定義維度中的實際資料。 屬性不一定會屬於某個階層，但是階層會從屬性建立而來。 階層會建立排序的層級清單，並定義一個方式讓使用者可瀏覽維度。  
  
## <a name="in-this-section"></a>本節內容  
 下列主題提供有關如何設計及實作維度物件的詳細資訊。  
  
|主題|Description|  
|-----------|-----------------|  
|[維度 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)|在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，維度是 cube 的基礎元件。 維度會以使用者希望了解的領域來組織資料，例如客戶、商店或員工。|  
|[屬性和屬性階層](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)|維度是屬性的集合，這些屬性會繫結至資料來源檢視中資料表或檢視內的一或多個資料行。|  
|[中，使用 [維度設計師] 的](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)|在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，維度內的屬性會一律直接或間接與相關的索引鍵屬性。 當您根據所有維度屬性都是衍生自相同關聯式資料表的星狀結構描述來定義維度時，便會在索引鍵屬性和維度的每個非索引鍵屬性之間，自動定義屬性關聯性。 而根據維度屬性是衍生自多個相關資料表的雪花式結構描述來定義維度時，便會自動定義下列的屬性關聯性：<br /><br /> 索引鍵屬性和繫結到主維度資料表之資料行的每個非索引鍵屬性之間。<br /><br /> 索引鍵屬性和繫結到連結基礎維度資料表之次要資料表的外部索引鍵屬性之間。<br /><br /> 在繫結到次要資料表之外部索引鍵的屬性和繫結到次要資料表中之資料行的非索引鍵屬性之間。|  
  
  

