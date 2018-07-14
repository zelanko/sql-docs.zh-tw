---
title: 查詢多維度資料與 MDX |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional data [Analysis Services], querying
ms.assetid: e0a5dd60-35a3-4a4f-b36f-52ecea814886
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4227c7a2483035c7fdf5ae472711ad0ea96c73bb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37212298"
---
# <a name="querying-multidimensional-data-with-mdx"></a>使用 MDX 查詢多維度資料
  多維度運算式 (MDX) 是用於 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]並從中擷取多維度資料的查詢語言。 MDX 是以 XML for Analysis (XMLA) 規格為基礎，具有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]的特定延伸模組。 MDX 利用由識別碼、值、陳述式、函數及運算子組成的運算式， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 可以評估該運算式來擷取物件 (例如集合或成員)，或擷取純量值 (例如字串或數字)。  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中，MDX 查詢和運算式可用來執行下列動作：  
  
-   將資料從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Cube 傳回至用戶端應用程式。  
  
-   格式化查詢結果。  
  
-   執行 Cube 設計工作，包括定義導出成員、命名集、範圍指派和關鍵效能指標 (KPI)。  
  
-   執行管理工作，包括維度和資料格安全性。  
  
 MDX 表面上在許多方面與一般用於關聯式資料庫的 SQL 語法非常類似。 然而，MDX 不是 SQL 語言的延伸模組，在許多方面與 SQL 有所不同。 若要建立用來設計或保護 Cube 的 MDX 運算式，或要建立 MDX 查詢以傳回和格式化多維度資料，您必須了解 MDX 和維度模型的基本概念、MDX 語法元素、MDX 運算子、MDX 陳述式及 MDX 函數。  
  
> [!NOTE]  
>  如需詳細資訊，請參閱 < 其他資源 區段上[SQL Server 2005 – Analysis Services](http://go.microsoft.com/fwlink/?LinkId=80853) Microsoft TechNet 網站上的頁面。 如需 MDX 查詢和計算相關效能問題的詳細資訊，請參閱 [SQL Server 2005 Analysis Services Performance Guide](http://go.microsoft.com/fwlink/?LinkId=81621)(SQL Server 2005 Analysis Services 效能指南) 的 “Writing Efficient MDX” (＜撰寫有效率的 MDX＞) 一節。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[重要的概念在 MDX 中的&#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)|您可以使用多維度運算式 (MDX) 來查詢多維度資料，或建立用於 Cube 內的 MDX 運算式，但首先您應該了解 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 維度概念和詞彙。|  
|[MDX 查詢基礎觀念&#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)|您可以使用多維度運算式 (MDX) 查詢多維度物件 (例如 Cube)，然後傳回包含 Cube 資料的多維度資料格集。 這個主題以及子主題將提供對 MDX 查詢的概觀。|  
|[MDX 指令碼基礎觀念&#40;Analysis Services&#41;](mdx-scripting-fundamentals-analysis-services.md)|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中，多維度運算式 (MDX) 指令碼是由一個或多個 MDX 運算式或陳述式構成，利用計算擴展 Cube。<br /><br /> MDX 指令碼可定義 Cube 的計算處理序。 MDX 指令碼也會被視為 Cube 本身的一部分。 因此，變更與 Cube 相關的 MDX 指令碼，會立即變更 Cube 的計算處理序。<br /><br /> 若要建立 MDX 指令碼，您可以使用 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中的 Cube 設計師。|  
  
## <a name="see-also"></a>另請參閱  
 [MDX 語法元素&#40;MDX&#41;](/sql/mdx/mdx-syntax-elements-mdx)   
 [MDX 語言參考&#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)  
  
  
