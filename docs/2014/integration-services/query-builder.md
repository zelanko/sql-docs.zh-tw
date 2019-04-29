---
title: 查詢產生器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.querybuilder.f1
helpviewer_keywords:
- Query Builder dialog box
ms.assetid: 780752c9-6e3c-4f44-aaff-4f4d5e5a45c5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e09e41535ad878a3f20ae74df07ace7bda6fa7e4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62889581"
---
# <a name="query-builder"></a>查詢產生器
  使用 **[查詢產生器]** 對話方塊，即可建立要在執行 SQL 工作中使用的查詢、OLE DB 來源和 OLE DB 目的地，以及查閱轉換。  
  
 您可以使用「查詢產生器」執行下列工作：  
  
-   **使用查詢的圖形表示法或使用 SQL 命令** ：「查詢產生器」包含以圖形方式顯示查詢的窗格，以及顯示查詢之 SQL 文字的窗格。 您可使用圖形窗格或文字窗格。 「查詢產生器」會同步檢視，讓它們始終保持最新狀態。  
  
-   **聯結相關的資料表** ：如果您將一個以上的資料表新增到查詢中，「查詢產生器」會自動決定如何與資料表產生關聯，並建構適當的聯結命令。  
  
-   **查詢或更新資料庫** ：您可以使用查詢產生器，藉由使用 Transact-SQL SELECT 陳述式傳回資料，並建立更新、新增或刪除資料庫中記錄的查詢。  
  
-   **立即檢視並編輯結果** ：您可以執行您的查詢並使用方格 (您可以捲動並編輯資料庫中的記錄) 中的資料錄集。  
  
 [查詢產生器] 對話方塊中的圖形工具，可以讓您使用拖放作業建構查詢。 依預設，[查詢產生器] 對話方塊會建構 SELECT 查詢，不過您也可以建立 INSERT、UPDATE 或 DELETE 查詢。 在 **[查詢產生器]** 對話方塊中，可以剖析和執行所有類型的 SQL 陳述式。 如需封裝中 SQL 陳述式的詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 查詢](integration-services-ssis-queries.md)。  
  
 若要深入了解 Transact-SQL 語言及其語法，請參閱 [Transact-SQL 參考 &#40;資料庫引擎&#41;](/sql/t-sql/language-reference)。  
  
 您也可以在查詢中使用變數以提供值給輸入參數、擷取輸出參數的值以及儲存傳回碼。 若要深入了解如何在套件所用的查詢中使用變數，請參閱[執行 SQL 工作](control-flow/execute-sql-task.md)、[OLE DB 來源](data-flow/ole-db-source.md)和 [Integration Services &#40;SSIS&#41; 查詢](integration-services-ssis-queries.md)。 若要深入了解如何在執行 SQL 工作中使用變數，請參閱 [執行 SQL 工作中的參數和傳回碼](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md) 和 [執行 SQL 工作中的結果集](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)。  
  
 「查閱」和「模糊」查閱轉換也可以使用具有參數和傳回碼的變數。 OLE DB 來源的相關資訊也適用於這兩個轉換。  
  
## <a name="options"></a>選項。  
 **工具列**  
 使用工具列來管理資料集、選取要顯示的窗格，以及控制查詢功能。  
  
|值|描述|  
|-----------|-----------------|  
|**顯示/隱藏圖表窗格**|顯示或隱藏 **[圖表]** 窗格。|  
|**顯示/隱藏方格窗格**|顯示或隱藏 **[方格]** 窗格。|  
|**顯示/隱藏 SQL 窗格**|顯示或隱藏 **[SQL]** 窗格。|  
|**顯示/隱藏結果窗格**|顯示或隱藏 **[結果]** 窗格。|  
|**執行**|執行查詢。 結果會顯示在結果窗格中。|  
|**驗證 SQL**|確認 SQL 陳述式有效。|  
|**遞增排序**|在方格窗格中之選取的資料行上，依遞增順序排序輸出資料列。|  
|**遞減排序**|在方格窗格中之選取的資料行上，依遞減順序排序輸出資料列。|  
|**移除篩選**|選取方格窗格中的某資料行名稱，然後按一下 **[移除篩選]** ，即可移除該資料行的排序準則。|  
|**使用群組依據**|將 GROUP BY 功能加入至查詢。|  
|**新增資料表**|將新的資料表加入至查詢。|  
  
 **查詢定義**  
 查詢定義會提供可在其中定義和測試查詢的工具列和窗格。  
  
|窗格|描述|  
|----------|-----------------|  
|**圖表** 窗格|在圖表中顯示查詢。 此圖表顯示查詢所包括的資料表及其聯結方式。 選取或清除資料表之資料行旁邊的核取方塊，以便在查詢輸出中加入或移除。<br /><br /> 將資料表加入查詢時，查詢產生器會依據資料表中的索引鍵來建立以資料表為基礎的資料表之間的聯結。 若要加入聯結，請將欄位從一個資料表拖曳至另一個資料表的欄位。 若要管理聯結，請以滑鼠右鍵按一下聯結，然後選取功能表選項。<br /><br /> 以滑鼠右鍵按一下 [圖表] 窗格，即可加入或移除資料表、選取所有資料表以及顯示或隱藏窗格。|  
|**方格** 窗格|在方格中顯示查詢。 您可以使用此方格，將資料行加入至查詢、從查詢移除資料行，以及變更每個資料行的設定。|  
|**SQL** 窗格|以 SQL 文字顯示查詢。 在 **[圖表]** 窗格和 **[方格]** 窗格中所做的變更會出現在此處，而在此處所做的變更會出現在 **[圖表]** 窗格和 **[方格]** 窗格中。|  
|**結果** 窗格|當您在工具列上按一下 **[執行]** 時，會顯示查詢的結果。|  
  
## <a name="see-also"></a>另請參閱  
 [執行 SQL 工作](control-flow/execute-sql-task.md)   
 [OLE DB 來源](data-flow/ole-db-source.md)   
 [OLE DB 目的地](data-flow/ole-db-destination.md)   
 [查閱轉換](data-flow/transformations/lookup-transformation.md)   
 [Integration Services &#40;SSIS&#41;查詢](integration-services-ssis-queries.md)   
 [Integration Services 套件中的 MERGE](control-flow/merge-in-integration-services-packages.md)  
  
  
