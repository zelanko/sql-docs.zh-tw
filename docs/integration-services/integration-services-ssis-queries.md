---
title: Integration Services (SSIS) 查詢 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.querybuilder.f1
helpviewer_keywords:
- Query Builder [Integration Services]
- queries [Integration Services]
- statements [Integration Services]
- queries [Integration Services], about queries in packages
ms.assetid: 8822bd29-4575-46c8-92a0-1a39bc2604c1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d24d4e8bdebca82ec0541132b52ac84de6c9c271
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284486"
---
# <a name="integration-services-ssis-queries"></a>Integration Services (SSIS) 查詢

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  「執行 SQL」工作、OLE DB 來源、OLE DB 目的地和「查閱」轉換可使用 SQL 查詢。 在「執行 SQL」工作中，SQL 陳述式可建立、更新和刪除資料庫物件和資料；執行預存程序；以及執行 SELECT 陳述式。 在 OLE DB 來源和「查閱」轉換中的 SQL 陳述式通常都是 SELECT 陳述式或 EXEC 陳述式。 後者最常執行傳回結果集的預存程序。  
  
 可以剖析查詢，以確定它是否有效。 剖析使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]連接的查詢時，會剖析和執行該查詢，並將執行結果 (成功或失敗) 指派給剖析結果。 如果查詢使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]以外的資料連接，就只會剖析陳述式。  
  
您可以使用下列方式提供 SQL 陳述式：
1.   直接在設計工具中輸入它。
2.   指定與包含此陳述式之檔案的連線。
3.   指定包含此陳述式的變數。  
  
## <a name="direct-input-sql"></a>直接輸入 SQL  
 「查詢產生器」可在「執行 SQL」工作、OLE DB 來源、OLE DB 目的地和「查閱」轉換的使用者介面上取得。 「查詢產生器」有下列優點：  
  
-   以視覺化方式或利用 SQL 命令工作。  
  
     「查詢產生器」包含以視覺化方式撰寫查詢的圖形窗格，以及顯示查詢之 SQL 文字的文字窗格。 您可使用圖形或文字窗格。 「查詢產生器」會同步處理檢視，讓查詢文字和圖形表示永遠都相符。  
  
-   聯結相關的資料表。  
  
     若您加入一個以上的資料表到查詢，「查詢產生器」會自動決定資料表相關的方式，並建構適當的聯結指令。  
  
-   查詢或更新資料庫。  
  
     您可以使用「查詢產生器」，利用 Transact-SQL SELECT 陳述式傳回資料，或建立更新、加入或刪除資料庫中資料錄的查詢。  
  
-   立即檢視並編輯結果。  
  
     您可以執行您的查詢並使用方格 (可讓您在資料庫中捲動並編輯資料錄) 中的資料錄集。  
  
 儘管「查詢產生器」受到視覺化方式的限制，只能建立 SELECT 查詢，但您可在文字窗格中輸入其他類型的 SQL 陳述式，例如，DELETE 和 UPDATE 陳述式。 圖形窗格會自動進行更新，以反映您所輸入的 SQL 陳述式。  
  
 您還可在工作或資料流程元件對話方塊或 [屬性] 視窗中輸入查詢，以提供直接輸入。  
  
 如需詳細資訊，請參閱 [查詢產生器](https://msdn.microsoft.com/library/780752c9-6e3c-4f44-aaff-4f4d5e5a45c5)。  
  
## <a name="sql-in-files"></a>檔案中的 SQL  
 「執行 SQL」工作的 SQL 陳述式也可位於個別檔案中。 例如，在執行封裝時，您可以使用工具 (例如， [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中的「查詢編輯器」) 撰寫查詢、將查詢儲存至檔案，然後從檔案讀取該查詢。 檔案只能包含要執行的 SQL 陳述式和註解。 若要使用在檔案中儲存的 SQL 陳述式，您必須提供指定檔案名稱和位置的檔案連接。 如需相關資訊，請參閱 [檔案連線管理員](../integration-services/connection-manager/file-connection-manager.md)。  
  
## <a name="sql-in-variables"></a>變數中的 SQL  
 如果「執行 SQL」工作中的 SQL 陳述式來源是一個變數，則您要提供包含查詢之變數的名稱。 變數的 Value 屬性包含查詢文字。 您可以將變數的 ValueType 屬性設為字串資料類型，然後將 SQL 陳述式輸入或複製到 Value 屬性中。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../integration-services/integration-services-ssis-variables.md)和[在封裝中使用變數](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)。  

## <a name="query-builder-dialog-box"></a>查詢產生器對話方塊
使用 **[查詢產生器]** 對話方塊，即可建立要在執行 SQL 工作中使用的查詢、OLE DB 來源和 OLE DB 目的地，以及查閱轉換。  
  
 您可以使用「查詢產生器」執行下列工作：  
  
-   **使用查詢的圖形表示法或使用 SQL 命令** ：「查詢產生器」包含以圖形方式顯示查詢的窗格，以及顯示查詢之 SQL 文字的窗格。 您可使用圖形窗格或文字窗格。 「查詢產生器」會同步檢視，讓它們始終保持最新狀態。  
  
-   **聯結相關的資料表** ：如果您將一個以上的資料表新增到查詢中，「查詢產生器」會自動決定如何與資料表產生關聯，並建構適當的聯結命令。  
  
-   **查詢或更新資料庫** ：您可以使用查詢產生器，藉由使用 Transact-SQL SELECT 陳述式傳回資料，並建立更新、新增或刪除資料庫中記錄的查詢。  
  
-   **立即檢視並編輯結果** ：您可以執行您的查詢並使用方格 (您可以捲動並編輯資料庫中的記錄) 中的資料錄集。  
  
 [查詢產生器]  對話方塊中的圖形工具，可以讓您使用拖放作業建構查詢。 依預設，[查詢產生器] 對話方塊會建構 SELECT 查詢，不過您也可以建立 INSERT、UPDATE 或 DELETE 查詢。 在 **[查詢產生器]** 對話方塊中，可以剖析和執行所有類型的 SQL 陳述式。 如需封裝中 SQL 陳述式的詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 查詢](../integration-services/integration-services-ssis-queries.md)。  
  
 若要深入了解 Transact-SQL 語言及其語法，請參閱 [Transact-SQL 參考 &#40;資料庫引擎&#41;](../t-sql/transact-sql-reference-database-engine.md)。  
  
 您也可以在查詢中使用變數以提供值給輸入參數、擷取輸出參數的值以及儲存傳回碼。 若要深入了解如何在套件所用的查詢中使用變數，請參閱[執行 SQL 工作](../integration-services/control-flow/execute-sql-task.md)、[OLE DB 來源](../integration-services/data-flow/ole-db-source.md)和 [Integration Services &#40;SSIS&#41; 查詢](../integration-services/integration-services-ssis-queries.md)。 若要深入了解如何在執行 SQL 工作中使用變數，請參閱 [執行 SQL 工作中的參數和傳回碼](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663) 和 [執行 SQL 工作中的結果集](https://msdn.microsoft.com/library/62605b63-d43b-49e8-a863-e154011e6109)。  
  
 「查閱」和「模糊」查閱轉換也可以使用具有參數和傳回碼的變數。 OLE DB 來源的相關資訊也適用於這兩個轉換。  
  
### <a name="options"></a>選項。  
 **工具列**  
 使用工具列來管理資料集、選取要顯示的窗格，以及控制查詢功能。  
  
|ReplTest1|Description|  
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
  
|窗格|Description|  
|----------|-----------------|  
|**圖表** 窗格|在圖表中顯示查詢。 此圖表顯示查詢所包括的資料表及其聯結方式。 選取或清除資料表之資料行旁邊的核取方塊，以便在查詢輸出中加入或移除。<br /><br /> 將資料表加入查詢時，查詢產生器會依據資料表中的索引鍵來建立以資料表為基礎的資料表之間的聯結。 若要加入聯結，請將欄位從一個資料表拖曳至另一個資料表的欄位。 若要管理聯結，請以滑鼠右鍵按一下聯結，然後選取功能表選項。<br /><br /> 以滑鼠右鍵按一下 [圖表]  窗格，即可加入或移除資料表、選取所有資料表以及顯示或隱藏窗格。|  
|**方格** 窗格|在方格中顯示查詢。 您可以使用此方格，將資料行加入至查詢、從查詢移除資料行，以及變更每個資料行的設定。|  
|**SQL** 窗格|以 SQL 文字顯示查詢。 在 **[圖表]** 窗格和 **[方格]** 窗格中所做的變更會出現在此處，而在此處所做的變更會出現在 **[圖表]** 窗格和 **[方格]** 窗格中。|  
|**結果** 窗格|當您在工具列上按一下 **[執行]** 時，會顯示查詢的結果。| 

  
