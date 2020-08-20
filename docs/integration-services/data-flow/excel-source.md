---
description: Excel 來源
title: Excel 來源 | Microsoft Docs
ms.custom: ''
ms.date: 05/15/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.excelsource.f1
- sql13.dts.designer.excelsourceadapter.connection.f1
- sql13.dts.designer.excelsourceadapter.columns.f1
- sql13.dts.designer.excelsourceadapter.erroroutput.f1
helpviewer_keywords:
- Excel [Integration Services]
- sources [Integration Services], Excel
ms.assetid: e66349f3-b1b8-4763-89b7-7803541a4d62
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9664786703f0d9b81ce2a939bd422ea41a2fd8f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484569"
---
# <a name="excel-source"></a>Excel 來源

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Excel 來源會從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 活頁簿中的工作表或範圍擷取資料。  

> [!IMPORTANT]
> 如需連接至 Excel 檔案，以及將資料從 Excel 檔案載入或載入至 Excel 檔案的限制與已知問題的詳細資訊，請參閱[使用 SQL Server Integration Services (SSIS) 將資料從 Excel 載入或載入至 Excel](../load-data-to-from-excel-with-ssis.md)。

## <a name="access-modes"></a>存取模式
 Excel 來源會提供四種不同的資料存取模式來擷取資料：  
  
-   資料表或檢視。  
  
-   在變數中指定的資料表或檢視。  
  
-   SQL 陳述式的結果。 查詢可以是參數化查詢。  
  
-   儲存在變數中之 SQL 陳述式的結果。  
  
 Excel 來源會使用 Excel 連接管理員連接到資料來源，而連接管理員會指定要使用的活頁簿檔案。 如需詳細資訊，請參閱 [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md)。  
  
 Excel 來源有一個一般輸出和一個錯誤輸出。  
  
## <a name="excel-source-configuration"></a>Excel 來源組態  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之所有屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Excel 自訂屬性](../../integration-services/data-flow/excel-custom-properties.md)  
  
 如需循環使用 Excel 檔案群組的資訊，請參閱 [使用 Foreach 迴圈容器來循環使用 Excel 檔案和資料表](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)。  
  
## <a name="excel-source-editor-connection-manager-page"></a>Excel 來源編輯器 (連接管理員頁面)
  使用 **[Excel 來源編輯器]** 對話方塊的 **[連接管理員]** 節點，以選取來源要使用的 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 活頁簿。 Excel 來源會從工作表或現有活頁簿的具名範圍中讀取資料。  
  
> [!NOTE]  
>  在 **[Excel 來源編輯器]** 中無法使用 Excel 來源的 **CommandTimeout**屬性，但可使用 **[進階編輯器]** 來設定這個屬性。 如需有關這個屬性的詳細資訊，請參閱＜ [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md)＞的＜Excel 來源＞一節。  
  
### <a name="static-options"></a>靜態選項  
 **[無快取]**  
 從清單中選取現有的 Excel 連線管理員，或按一下 [新增]**** 建立新的連線管理員。  
  
 **新增**  
 使用 [Excel 連線管理員]**** 對話方塊來建立新的連線管理員。  
  
 **資料存取模式**  
 從來源中指定選取資料的方法。  
  
|值|描述|  
|-----------|-----------------|  
|資料表或檢視|從工作表或 Excel 檔案的具名範圍中擷取資料。|  
|資料表名稱或檢視名稱變數|在變數中指定工作表或範圍名稱。<br /><br /> **相關資訊：** [在套件中使用變數](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|SQL (命令)|使用 SQL 查詢從 Excel 檔案中擷取資料。 |  
|來自變數的 SQL 命令|在變數中指定 SQL 查詢文字。|  
  
 **預覽**  
 使用 [資料檢視]  對話方塊來預覽結果。 預覽最多可顯示 200 個資料列。  
  
### <a name="data-access-mode-dynamic-options"></a>資料存取模式動態選項  
  
#### <a name="data-access-mode--table-or-view"></a>資料存取模式 = 資料表或檢視  
 **Excel 工作表的名稱**  
 從 Excel 活頁簿的可用工作表或具名範圍清單中，選取工作表或具名範圍的名稱。  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>資料存取模式 = 資料表名稱或檢視名稱變數  
 **變數名稱**  
 選取包含工作表名稱或具名範圍的變數。  
  
#### <a name="data-access-mode--sql-command"></a>資料存取模式 = SQL 命令  
 **SQL 命令文字**  
 輸入 SQL 查詢的文字，按一下 [建立查詢]**** 建立查詢，或按一下 [瀏覽]**** 瀏覽至包含查詢文字的檔案。  
  
 **參數**  
 如果您所輸入的參數化查詢使用 ? 做為查詢文字中的參數預留位置，請使用 **[設定查詢參數]** 對話方塊，將查詢輸入參數對應到封裝變數。  
  
 **建立查詢**  
 使用 [查詢產生器]  對話方塊，以視覺化的方式來建構 SQL 查詢。  
  
 **瀏覽**  
 使用 [開啟]  對話方塊來找出包含 SQL 查詢文字的檔案。  
  
 **剖析查詢**  
 請確認查詢文字的語法。  
  
#### <a name="data-access-mode--sql-command-from-variable"></a>資料存取模式 = 來自變數的 SQL 命令  
 **變數名稱**  
 選取包含 SQL 查詢文字的變數。  
  
## <a name="excel-source-editor-columns-page"></a>Excel 來源編輯器 (資料行頁面)
  使用 [Excel 來源編輯器]**** 對話方塊的 [資料行]**** 頁面，將輸出資料行對應至每個外部 (來源) 資料行。  
  
### <a name="options"></a>選項。  
 **可用的外部資料行**  
 在資料來源中檢視可用的外部資料行清單。 您無法使用此資料表來加入或刪除資料行。  
  
 **[外部資料行]**  
 依工作讀取外部 (來源) 資料行的順序來檢視它們。 首先取消選取上述資料表中選取的資料行，然後依不同順序從清單中選取外部資料行，就可以變更此順序。  
  
 **輸出資料行**  
 為每個輸出資料行提供唯一的名稱。 預設值為選取的外部 (來源) 資料行的名稱；不過，您也可以選擇任何唯一的、描述性的名稱。 提供的名稱將顯示在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師內。  
  
## <a name="excel-source-editor-error-output-page"></a>Excel 來源編輯器 (錯誤輸出頁面)
  使用 [Excel 來源編輯器]**** 對話方塊的 [錯誤輸出]**** 頁面，以選取錯誤處理選項，並設定錯誤輸出資料行上的屬性。  
  
### <a name="options"></a>選項。  
 **輸入或輸出**  
 檢視資料來源的名稱。  
  
 **資料行**  
 檢視您在 [Excel 來源編輯器]**** 對話方塊的 [連線管理員]**** 頁面上所選取的外部 (來源) 資料行。  
  
 **錯誤**  
 指定錯誤發生時要採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **相關主題：** [資料中的錯誤處理](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **截斷**  
 指定截斷發生時要採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **說明**  
 檢視錯誤的描述。  
  
 **將這個值設定到選取的資料格**  
 指定發生錯誤或截斷時要對所有選取之資料格採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **套用**  
 將錯誤處理選項套用至選取的資料格。  
  
## <a name="related-content"></a>相關內容  
[使用 SQL Server Integration Services (SSIS) 將資料從 Excel 載入或載入至 Excel](../load-data-to-from-excel-with-ssis.md)  
[Excel 目的地](excel-destination.md)  
[Excel 連線管理員](../connection-manager/excel-connection-manager.md)
