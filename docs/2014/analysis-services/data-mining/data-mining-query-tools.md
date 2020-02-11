---
title: 資料採礦查詢介面 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- predictions [Analysis Services], DMX prediction queries
- predictions [DMX]
- DMX [Analysis Services], prediction queries
- prediction queries [DMX]
- predictions [Analysis Services]
- queries [DMX], prediction queries
- mining models [Analysis Services], DMX
ms.assetid: a8952427-fd8c-4300-8f62-25f57ac1be0c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7c59d3a18c1fd36f82e8ea60e42d1b9f6e2f34c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084974"
---
# <a name="data-mining-query-interfaces"></a>資料採礦查詢介面
  資料採礦查詢是以資料採礦延伸模組 (DMX) 語言為基礎。 您可以針對所有預測和模型工作使用 DMX，包括分類、風險分析、產生建議及線性迴歸。 您也可以擷取處理模型時所產生的模式和統計資料。  
  
 使用 DMX 的預測查詢語法與 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的查詢語法類似。 
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 都提供協助您建立 DMX 預測查詢的工具。  
  
 此主題描述您可以透過 DMX 用來建立及執行資料採礦查詢的介面。  
  
 [查詢工具](#bkmk_Tools)  
  
-   [預測查詢產生器](#bkmk_Builder)  
  
-   [查詢編輯器](#bkmk_QueryEditor)  
  
-   [DMX 範本](#bkmk_Templates)  
  
-   [Integration Services](#bkmk_SSIS)  
  
 [應用程式設計介面](#bkmk_API)  
  
##  <a name="bkmk_Tools"></a>資料採礦查詢工具  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會提供下列工具，這些工具可讓您用來針對資料採礦物件建立預測查詢、內容查詢和資料定義查詢：  
  
-   預測查詢產生器  
  
-   查詢編輯器  
  
-   DMX 範本  
  
-   Integration Services 資料採礦元件  
  
###  <a name="bkmk_Builder"></a>預測查詢產生器  
 預測查詢產生器包含在資料採礦設計師 (** 和 ** 都有提供) 的 [採礦模型預測][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)][!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 索引標籤中。  
  
 在使用查詢產生器時，可以使用圖形工具來選取採礦模型、加入新的案例資料以及加入預測函數。 [預測查詢產生器] 包含可讓您手動修改查詢的文字編輯器，以及用來查看查詢結果的簡單 [**結果**] 窗格。  
  
###  <a name="bkmk_QueryEditor"></a>查詢編輯器  
 中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的查詢編輯器會提供工具，讓您用來建立及執行 DMX 查詢。 您可以連接到 SQL Server Analysis Services 的執行個體，然後選取資料庫、採礦結構資料行和採礦模型。 中繼資料總管**** 包含您可以瀏覽的預測函數清單。  
  
###  <a name="bkmk_Templates"></a>DMX 範本  
 
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供互動式的 DMX 查詢範本，可用來建立 DMX 查詢。 如果您看不到範本清單，請按一下工具列上的 [檢視]****，然後選取 [範本總管]****。 若要查看所有 Analysis Services 範本 (包括 DMX、MDX 及 XMLA 的範本)，請按一下 Cube 圖示。  
  
 若要使用範本建立查詢，您可以將範本拖曳到開啟的查詢視窗，也可以按兩下範本，開啟新的連接和新的查詢窗格。  
  
 如需如何根據範本建立預測查詢的範例，請參閱 [根據範本建立單一預測查詢](create-a-singleton-prediction-query-from-a-template.md)。  
  
> [!WARNING]  
>  適用於 Microsoft Office Excel 的資料採礦增益集也包含許多範本，連同可幫助您撰寫複雜 DMX 陳述式的互動式查詢產生器。 若要使用範本，請在資料採礦用戶端中按一下 [查詢]****，再按一下 [進階]****。  
  
###  <a name="bkmk_SSIS"></a>Integration Services 資料採礦元件  
 您也可以將[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]預測查詢包含為封裝的一部分。 
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的下列工作和轉換支援 DMX 預測查詢和 DMX 陳述式的建立及執行。  
  
|元件|描述|  
|---------------|-----------------|  
|資料採礦查詢工作|執行 DMX 查詢和其他 DMX 陳述式當做控制流程的一部分。<br /><br /> 工作編輯器提供預測查詢產生器，以及用來手動修改 DMX 查詢的文字方塊。 但是，工作編輯器無法根據 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 方案中的物件驗證查詢。 因此，最好在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 或 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中建立查詢，然後將陳述式或查詢文字貼入工作編輯器。|  
|資料採礦查詢轉換|使用資料流程來源所提供的資料，在資料流程內執行預測查詢。<br /><br /> 工作編輯器提供預測查詢產生器，以及用來手動修改 DMX 查詢的文字方塊。<br /><br /> 轉換只能用於建立使用資料流程中之資料的查詢，也就是使用 PREDICTION JOIN 語法的查詢。 此元件不能用於執行內容查詢或其他類型的 DMX 陳述式。|  
  
##  <a name="bkmk_API"></a>應用程式設計介面  
 您可以搭配 OLE DB 或 Analysis Services ADOMD 用戶端等伺服器通訊協定使用各種程式語言，建立針對資料採礦模型執行查詢的自訂應用程式。 如需詳細資訊，請參閱 [資料採礦程式設計](../dev-guide/data-mining-programming.md)。  
  
 不過，XMLA 會構成與 Analysis Service 伺服器之所有互動的基礎訊息格式。 在 XMLA 訊息內，查詢的表示方式會根據您傳送的是以 DMX 為基礎的預測查詢、內容查詢，或使用資料採礦結構描述資料列集擷取模型中繼資料的查詢而有所不同。  
  
-   
  **預測查詢** (及所有其他 DMX 陳述式) 的文字會使用 [Execute 方法 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) 方法以 XMLA 傳送，並將 DMX 查詢作為文字放在 XMLA [Command 元素 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) 元素的 [Statement 元素 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/command-element-xmla) 內。  
  
-   若要擷取**模型內容**和**模型中繼資料** (例如叢集數、決策樹中所使用的屬性、模型上次處理的日期及建立模型時所使用的演算法參數)，您可以使用 [Discover 方法 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) 方法，並在 [RequestType 元素 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla) 標頭中指定其中一個資料採礦結構描述資料列集。 若要縮小查詢範圍，請輸入準則作為 [RestrictionList 元素 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictionlist-element-xmla) 元素內的限制。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 參考](/sql/dmx/data-mining-extensions-dmx-reference)   
 [資料採礦解決方案](data-mining-solutions.md)   
 [瞭解 DMX Select 語句](/sql/dmx/understanding-the-dmx-select-statement)   
 [DMX 預測查詢的結構和使用方式](/sql/dmx/structure-and-usage-of-dmx-prediction-queries)   
 [使用預測查詢產生器來建立預測查詢](create-a-prediction-query-using-the-prediction-query-builder.md)   
 [在 SQL Server Management Studio 中建立 DMX 查詢](create-a-dmx-query-in-sql-server-management-studio.md)  
  
  
