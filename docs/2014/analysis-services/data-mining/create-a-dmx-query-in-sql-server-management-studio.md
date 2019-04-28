---
title: SQL Server Management Studio 中建立 DMX 查詢 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- templates [Analysis Services], queries
- SQL Server Management Studio [Analysis Services], DMX queries
- predictions [Analysis Services], DMX prediction queries
- predictions [DMX]
- prediction queries [DMX]
- queries [DMX], prediction queries
- mining models [Analysis Services], DMX
ms.assetid: 568ce40a-1f53-47eb-8c79-14347cdfde83
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c68e181a1ad0992e85c638accad26a0418be4b5e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62715345"
---
# <a name="create-a-dmx-query-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中建立 DMX 查詢
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供一組功能，可幫助您針對採礦模型和採礦結構建立預測查詢、內容查詢和資料定義查詢。  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中都有提供圖形化預測查詢產生器，可簡化撰寫預測查詢以及將資料集對應至模型的程序。  
  
-   [範本總管] 中所提供的查詢範本會開始建立許多種類的 DMX 查詢，包括許多類型的預測查詢。 內容查詢、使用巢狀資料集的查詢、從採礦結構傳回案例的查詢，甚至是資料定義查詢都有提供範本。  
  
-   MDX 和 DMX 查詢窗格中的 [中繼資料總管] 會提供可用模型和結構的清單 (您可以將其拖放到查詢產生器) 及 DMX 函數的清單。 這項功能可讓您輕鬆獲得正確的物件名稱，而不需要輸入。  
  
 本主題描述如何使用 [中繼資料總管] 和 DMX 查詢編輯器來建立 DMX 查詢。  
  
##  <a name="BKMK_Templates"></a> DMX 查詢範本  
 [範本總管] 有提供用來建立基本 DMX 查詢的範本。 [DMX] 資料夾包含資料採礦範本，這些範本分成以下類別：  
  
-   **模型內容**  
  
-   **模型管理**  
  
-   **預測查詢**  
  
-   **結構內容**  
  
 您也可以針對經常執行的查詢或命令建立自訂範本。  
  
## <a name="xmla-query-templates"></a>XMLA 查詢範本  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 也提供 XMLA 查詢的範本。  
  
 您可以使用 XMLA 和 DMX 執行的查詢類型之間有一些重疊。 例如，您可以使用 DMX 或資料採礦結構描述資料列集來建立某些模型內容查詢，但是結構描述資料列集有時會包含未在 DMX 內容查詢中公開的資訊。  
  
 在 DMX 和 XMLA 中處理作業的方式也有一些重大差異。 例如，您可以使用 XMLA 來執行管理作業 (例如備份整個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫)，但是如果您要備份單一採礦模型，DMX 會提供單一命令 [EXPORT &#40;DMX&#41;](/sql/dmx/export-dmx)，這個命令比較適合這個用途。  
  
##  <a name="BKMK_Building_Queries"></a> 建立及執行 DMX 查詢  
  
#### <a name="open-a-new-dmx-query-window"></a>開啟新的 DMX 查詢視窗  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中按一下 [新增查詢]，然後選取 [新增 Analysis Server DMX 查詢]。  
  
2.  當 [連接到伺服器] 對話方塊出現時，請選取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體，其中包含您要使用的採礦模型。  
  
#### <a name="open-template-explorer"></a>開啟範本總管  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的 [檢視] 功能表上，選取 [範本總管]。  
  
2.  按一下 [Analysis Server]，即可查看要套用至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 之範本的樹狀檢視。  
  
#### <a name="apply-a-template-to-build-a-query"></a>套用範本來建立查詢  
  
-   以滑鼠右鍵按一下適當的查詢類型，然後選取 [開啟]。  
  
-   或者將範本拖曳到查詢編輯器。  
  
-   您也可以使用 [查詢] 功能表上的 [指定參數值] 選項，填入查詢的參數。  
  
 如需如何從範本建立特定查詢類型的範例，請參閱以下主題：  
  
 [根據範本建立單一預測查詢](create-a-singleton-prediction-query-from-a-template.md)  
  
 [建立採礦模型內容查詢](create-a-content-query-on-a-mining-model.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦查詢介面](data-mining-query-tools.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 參考](/sql/dmx/data-mining-extensions-dmx-reference)  
  
  
