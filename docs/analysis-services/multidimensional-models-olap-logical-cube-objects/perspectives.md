---
title: "檢視方塊 |Microsoft 文件"
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
- ready-only cube view
- OLAP objects [Analysis Services], perspectives
- storing data [Analysis Services], perspectives
- perspectives [Analysis Services]
- cubes [Analysis Services], perspectives
- visibility [Analysis Services]
- storage [Analysis Services], perspectives
ms.assetid: b064171e-b1b4-4f32-95e5-59e1b831c4c9
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 798a8d872b52c21d794e3d1f21cf52e133d56277
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="perspectives"></a>檢視方塊
  檢視方塊是可讓使用者以更簡單的方式查看 Cube 的定義。 檢視方塊是 Cube 功能的子集。 檢視方塊可讓管理員建立 Cube 的檢視，幫助使用者將焦點放在最相關的資料上。 檢視方塊包含了 Cube 中所有物件的子集。 檢視方塊不能包含父 Cube 中未定義的元素。  
  
 簡單的 <xref:Microsoft.AnalysisServices.Perspective> 物件是由以下項目所組成：基本資訊、維度、量值群組、計算、KPI 和動作。 基本資訊包括檢視方塊的名稱和預設量值。 維度是 Cube 維度的子集。 量值群組是 Cube 量值群組的子集。 計算是 Cube 計算的子集。 KPI 是 Cube KPI 的子集。 動作是 Cube 動作的子集。  
  
 Cube 必須要先更新及處理，然後才可以使用檢視方塊。  
  
 Cube 可以是很複雜的物件，讓使用者在瀏覽[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 單一 Cube 可以代表整個資料倉儲的內容，且 Cube 中的多個量值群組代表多份事實資料表，而多個維度的基礎是多份維度資料表。 雖然這類 Cube 可以十分複雜且功能強大，但是對只需要與 Cube 的一小部份進行互動以滿足其商業智慧和報表需求的使用者而言，卻令人望而怯步。  
  
 在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，您可以使用檢視方塊來減少中之 cube 的複雜度[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 檢視方塊會定義可檢視之 Cube 子集，而這類子集會對 Cube 提供有焦點的商務特有或應用程式特有觀點； 檢視方塊會控制 Cube 所容納之物件的可見性。 下列物件可以在檢視方塊中顯示或隱藏：  
  
-   維度  
  
-   屬性  
  
-   階層  
  
-   量值群組  
  
-   量值  
  
-   關鍵效能指標 (KPI)  
  
-   計算 (導出成員、命名集和指令碼命令)  
  
-   動作  
  
 例如， **Adventure Works** cube 中[!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)]範例[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫包含十一個量值群組和二十一個不同的 cube 維度，代表銷售、 銷售預測和財務資料。 用戶端應用程式可以直接參考整個 Cube，但是這個觀點對於只想嘗試擷取基本銷售預測資訊的使用者而言可能不適合。 相反地，相同的使用者可以使用**銷售目標**的檢視限制的檢視方塊**Adventure Works** cube 只與銷售預測相關的物件。  
  
 在 Cube 中，使用者無法透過檢視方塊看到的物件，仍可以使用 XML for Analysis (XMLA)、多維度運算式 (MDX) 或資料採礦延伸模組 (DMX) 陳述式直接予以參考和擷取。 檢視方塊並不會限制 Cube 中物件的存取，而且也不應該這麼做；而檢視方塊是用來提供使用者較佳的 Cube 存取經驗。  
  
 檢視方塊是 Cube 的唯讀檢視；使用檢視方塊並無法重新命名或變更 Cube 中的物件。 同樣地，使用檢視方塊也無法變更 Cube 的行為或功能 (例如，使用視覺化總計)。  
  
## <a name="security"></a>安全性  
 檢視方塊並非用來作為安全性機制，而是在商業智慧應用程式中提供較佳使用者體驗的工具。 特定檢視方塊的所有安全性，都是繼承自基礎 Cube。 例如，如果使用者沒有 Cube 中物件的存取權，則檢視方塊也無法提供該物件的存取權。 必須先解決 Cube 的安全性，才能透過檢視方塊提供 Cube 中物件的存取權。  
  
  

