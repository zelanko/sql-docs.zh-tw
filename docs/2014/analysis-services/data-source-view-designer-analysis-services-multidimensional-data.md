---
title: 資料來源視圖設計工具（Analysis Services-多維度資料） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.f1
helpviewer_keywords:
- Data Source View Designer
ms.assetid: 6f40a074-761f-440b-a999-09b755bd86ce
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9153a2d07653872ca6ce1f90e39c90f32da21fba
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66082516"
---
# <a name="data-source-view-designer-analysis-services---multidimensional-data"></a>資料來源檢視設計工具 (Analysis Services - 多維度資料)
  資料來源檢視 (DSV) 是外部關聯式資料來源的邏輯檢視，用來建立多維度模型中的 Cube 和維度。  
  
 在產生 DSV 之後，您可以在 **中使用** [資料來源檢視設計工具] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ，直接處理 DSV，如果基礎資料來源遺漏了多維度模型所需的資料元素，這個方法很實用。  
  
 若要開啟 **[資料來源檢視設計工具]** ：  
  
-   在方案總管**** 中按兩下資料來源檢視。  
  
-   以滑鼠右鍵按一下方案總管**** 中的資料來源檢視，然後選取 [開啟]**** 或 [檢視表設計工具]****。  
  
 
  **[資料來源檢視設計工具]** 包含工具列、顯示 DSV 物件和關聯性的圖表、按照字母順序列出資料表和具名查詢的資料表窗格，以及用來建立及檢視 DSV 的特定圖表的 [圖表組合管理] 窗格。 您可以用滑鼠右鍵按一下資料表或關聯性，存取內容相關的命令。  
  
 ![資料來源檢視設計工具](media/ssas-dsvdesigner.PNG "資料來源檢視設計工具")  
  
 基本上，DSV 會顯示在處理期間要用來擴展模型物件的關聯式資料庫資料表。 DSV 通常是使用資料來源檢視精靈產生。 DSV 中的資料表、資料行和關聯性會成為 Cube 維度和量值的基礎。 一旦建立 DSV，您可以使用資料來源檢視設計工具來修改它。  
  
 大部分 Analysis Services 開發人員直接使用產生的 DSV，極少自訂。 如果來源資料來自於 SQL Server 資料庫檢視，這更是特別常見。 在此情況下，您可能會想在 T-SQL 檢視中管理資料關聯性和計算，而不是 Analysis Services DSV。 不過，如果您不是基礎資料庫的擁有者，您可以在 Analysis Services 中修改 DSV，進一步開發模型中所使用的資料結構。  
  
## <a name="tasks-in-data-source-view-designer"></a>資料來源檢視設計工具中的工作  
 使用資料來源檢視設計工具，您可以對 DSV 執行下列編輯：  
  
|||  
|-|-|  
|重新命名資料行或資料表，或建立新的導出資料行。 例如，將姓氏和名字串連成新的全名資料行。|[定義資料來源視圖中的已命名計算 &#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)|  
|手動加入資料表關聯性|[在資料來源視圖中定義邏輯關聯性 &#40;Analysis Services&#41;](multidimensional-models/define-logical-relationships-in-a-data-source-view-analysis-services.md)|  
|建立具名查詢，依據 T-SQL 查詢定義新物件。|[在資料來源視圖中定義已命名的查詢 &#40;Analysis Services&#41;](multidimensional-models/define-named-queries-in-a-data-source-view-analysis-services.md)|  
|瀏覽基礎資料，檢視模型物件所代表的實際資料值。<br /><br /> 資料瀏覽可讓您以視覺化方式檢查及複製從基礎維度資料表或查詢傳回的資料。 根據預設，資料瀏覽使用最高計數取樣方法，取樣計數為 5000，但是您可以修訂這些設定。|[流覽資料來源視圖中的資料 &#40;Analysis Services&#41;](multidimensional-models/explore-data-in-a-data-source-view-analysis-services.md)|  
|將 DSV 中全部或部分的資料表和關聯性建立成圖表|[在資料來源視圖設計工具中使用圖表 &#40;Analysis Services&#41;](multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)|  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的資料來源視圖](multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [在資料來源 View 中加入或移除資料表或視圖 &#40;Analysis Services&#41;](multidimensional-models/adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md)  
  
  
