---
title: 維度物件 (Analysis Services-多維度資料) |Microsoft 文件
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- dimensions [Analysis Services], objects
ms.assetid: 7f3d55c7-cccb-4ad0-b6cb-3a2c9992dd68
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0ef31622b9b158ee55c4f31b437c1fed4679ad19
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036909"
---
# <a name="dimension-objects-analysis-services---multidimensional-data"></a>維度物件 (Analysis Services - 多維度資料)
  簡單 <xref:Microsoft.AnalysisServices.Dimension> 物件是由基本資訊、屬性和階層所組成。 基本資訊包括維度的名稱、維度的類型、資料來源、儲存模式等等。 屬性會定義維度中的實際資料。 屬性不一定會屬於某個階層，但是階層會從屬性建立而來。 階層會建立排序的層級清單，並定義一個方式讓使用者可瀏覽維度。  
  
## <a name="in-this-section"></a>本節內容  
 下列主題提供有關如何設計及實作維度物件的詳細資訊。  
  
|主題|描述|  
|-----------|-----------------|  
|[維度 &#40;Analysis Services-多維度資料 &#41;](dimensions-analysis-services-multidimensional-data.md)|在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，維度是 cube 的基礎元件。 維度會以使用者希望了解的領域來組織資料，例如客戶、商店或員工。|  
|[屬性和屬性階層](attributes-and-attribute-hierarchies.md)|維度是屬性的集合，這些屬性會繫結至資料來源檢視中資料表或檢視內的一或多個資料行。|  
|[屬性關聯性](attribute-relationships.md)|在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，維度內的屬性會一律直接或間接與相關的索引鍵屬性。 當您根據所有維度屬性都是衍生自相同關聯式資料表的星狀結構描述來定義維度時，便會在索引鍵屬性和維度的每個非索引鍵屬性之間，自動定義屬性關聯性。 而根據維度屬性是衍生自多個相關資料表的雪花式結構描述來定義維度時，便會自動定義下列的屬性關聯性：<br /><br /> -之間的索引鍵屬性和每個非索引鍵屬性繫結至主維度資料表中的資料行。<br />-索引鍵的屬性和繫結到次要資料表中的外部索引鍵屬性之間的連結基礎維度資料表。<br />-之間屬性次要資料表和每個非索引鍵屬性中的繫結至外部索引鍵繫結至資料行從第二個資料表。|  
  
  