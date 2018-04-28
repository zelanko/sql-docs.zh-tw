---
title: OLE DB 來源 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.oledbsource.f1
- sql13.dts.designer.oledbsourceadapter.connection.f1
- sql13.dts.designer.oledbsourceadapter.columns.f1
- sql13.dts.designer.oledbsourceadapter.errorhandling.f1
helpviewer_keywords:
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: f87cc5f6-b078-40f3-9d87-7a65e13e4c86
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 19d35698d556adc467fc96fe72ff391e2d6b44b0
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="ole-db-source"></a>OLE DB 來源
  OLE DB 來源會使用資料庫資料表、檢視或 SQL 命令，從各種 OLE DB 相容的關聯式資料庫中擷取資料。 例如，OLE DB 來源可從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的資料表中擷取資料。  
  
> [!NOTE]  
>  如果資料來源為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007，則資料來源需要舊版 Excel 以外的連接管理員。 如需詳細資訊，請參閱 [連接至 Excel 活頁簿](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)。  
  
 OLE DB 來源提供四種不同的資料存取模式用來擷取資料：  
  
-   資料表或檢視。  
  
-   在變數中指定的資料表或檢視。  
  
-   SQL 陳述式的結果。 查詢可以是參數化查詢。  
  
-   儲存在變數中之 SQL 陳述式的結果。  
  
> [!NOTE]  
>  當您使用 SQL 陳述式呼叫從暫存資料表傳回結果的預存程序時，請使用 WITH RESULT SETS 選項定義結果集的中繼資料。  
  
 如果使用參數化查詢，您可以將變數對應到參數，以指定 SQL 陳述式中個別參數的值。  
  
 此來源使用 OLE DB 連接管理員連接到資料來源，且連接管理員會指定要使用的 OLE DB 提供者。 如需詳細資訊，請參閱 [OLE DB 連線管理員](../../integration-services/connection-manager/ole-db-connection-manager.md)。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案也提供資料來源物件，您可從中建立 OLE DB 連接管理員，並提供資料來源和資料檢視讓 OLE DB 來源使用。  
  
 根據 OLE DB 提供者而定，下列限制適用 OLE DB 來源：  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB provider for Oracle 不支援 Oracle 資料類型 BLOB、CLOB、NCLOB、BFILE 或 UROWID，且 OLE DB 來源無法從含有這些資料類型之資料行的資料表擷取資料。  
  
-   IBM OLE DB DB2 提供者和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB DB2 提供者不支援使用呼叫預存程序的 SQL 命令。 使用這類命令時，OLE DB 來源無法建立資料行中繼資料，結果在資料流程中跟隨 OLE DB 來源的資料流程元件便沒有任何可用的資料行資料，且資料流程執行失敗。  
  
 OLE DB 來源有一個一般輸出和一個錯誤輸出。  
  
## <a name="using-parameterized-sql-statements"></a>使用參數化 SQL 陳述式。  
 OLE DB 來源可以使用 SQL 陳述式來擷取資料。 該陳述式可以是 SELECT 或 EXEC 陳述式。  
  
 OLE DB 來源使用 OLE DB 連接管理員，以連接到其擷取資料的資料來源。 根據 OLE DB 連接管理員使用的提供者以及連接管理員所連接的關聯式資料庫管理系統 (RDBMS) 而定，參數的命名和列示可能適用不同的規則。 如果從 RDBMS 傳回參數名稱，您可以使用參數名稱，將參數清單中的參數對應到 SQL 陳述式中的參數；否則，參數便會按照它們在參數清單中的序數位置，對應到 SQL 陳述式中的參數。 支援的參數名稱類型會因提供者而不同。 例如，某些提供者要求您必須使用變數或資料行名稱，而某些提供者則要求您使用 0 或 Param0 之類的符號名稱。 如需有關在 SQL 陳述式中使用之參數名稱的資訊，請參考提供者專用的文件集。  
  
 您在使用 OLE DB 連接管理員時無法使用參數化的子查詢，因為 OLE DB 來源無法透過 OLE DB 提供者衍生參數資訊。 不過，您可以使用運算式來將參數值串連到查詢字串中並設定來源的 SqlCommand 屬性。在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中，則可使用 [OLE DB 來源編輯器] 對話方塊來設定 OLE DB 來源，並在 [設定查詢參數] 對話方塊中將參數對應到變數。  
  
### <a name="specifying-parameters-by-using-ordinal-positions"></a>使用序數位置指定參數  
 如果沒有傳回任何參數名稱，便會依照參數在 [設定查詢參數] 對話方塊之 [參數] 清單中的列示順序，來控制執行階段中參數所對應的參數標記。 清單中的第一個參數會對應到 SQL 陳述式裡的第一個 ?， 第二個參數則對應到第二個 ?，依此類推。  
  
 下列 SQL 陳述式會從 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 資料庫的 **Product** 資料表中選取資料列。 [對應] 清單中的第一個參數對應到 **Color** 資料行的第一個參數，第二個參數則對應到 **Size** 資料行。  
  
 `SELECT * FROM Production.Product WHERE Color = ? AND Size = ?`  
  
 參數名稱無效。 例如，如果參數名稱與它所套用的資料行名稱相同，但並未放在 [參數] 清單中的正確序數位置，則執行階段中發生的參數對應將會使用參數的序數位置，而非參數名稱。  
  
 EXEC 命令通常會要求您使用在程序中提供參數值的變數名稱作為參數名稱。  
  
### <a name="specifying-parameters-by-using-names"></a>使用名稱指定參數  
 如果由 RDBMS 傳回實際參數名稱，SELECT 和 EXEC 陳述式所使用的參數便會依照名稱進行對應。 參數名稱必須符合 SELECT 陳述式或 EXEC 陳述式執行之預存程序所預期的名稱。  
  
 下列 SQL 陳述式會執行 **uspGetWhereUsedProductID** 預存程序，您可在 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 資料庫中找到該預存程序。  
  
 `EXEC uspGetWhereUsedProductID ?, ?`  
  
 預存程序需要有變數 `@StartProductID` 和 `@CheckDate`，才能提供參數值。 參數出現在 [對應] 清單中的順序並無任何影響。 唯一的需求是參數名稱必須符合預存程序中的變數名稱，包括 @ 符號。  
  
### <a name="mapping-parameters-to-variables"></a>將參數對應至變數  
 參數會對應到在執行階段中提供參數值的變數。 這些變數通常是使用者自訂變數，不過您也可以使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的系統變數。 如果您使用的是使用者自訂變數，請務必將資料類型設定為與對應參數所參考之資料行資料類型相容的類型。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)。  
  
## <a name="troubleshooting-the-ole-db-source"></a>疑難排解 OLE DB 來源  
 您可以記錄 OLE DB 來源對外部資料提供者所執行的呼叫。 您可以使用這項記錄功能，疑難排解 OLE DB 來源執行的從外部資料來源載入資料的作業。 若要記錄 OLE DB 來源對外部資料提供者執行的呼叫，請啟用封裝記錄，然後在封裝層級選取 [診斷] 事件。 如需詳細資訊，請參閱 [封裝執行的疑難排解工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="configuring-the-ole-db-source"></a>設定 OLE DB 來源  
 您可以程式設計方式或透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [OLE DB 自訂屬性](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
## <a name="related-tasks"></a>相關工作  
  
-   [使用 OLE DB 來源來擷取資料](../../integration-services/data-flow/extract-data-by-using-the-ole-db-source.md)  
  
-   [在資料流程元件中將查詢參數對應至變數](../../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [設定資料流程元件的屬性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [排序合併和合併聯結轉換的資料](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-content"></a>相關內容  
 social.technet.microsoft.com 上的 Wiki 文章： [SSIS with Oracle Connectors](http://go.microsoft.com/fwlink/?LinkId=220670)(SSIS 與 Oracle 連接器)。  
  
## <a name="ole-db-source-editor-connection-manager-page"></a>OLE DB 來源編輯器 (連接管理員頁面)
  使用 [OLE DB 來源編輯器] 對話方塊的 [連接管理員] 頁面，來選取來源的 OLE DB 連接管理員。 這個頁面也可以讓您從資料庫中選取資料表或檢視。  
  
> [!NOTE]  
>  若要從使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 的資料來源載入資料，請使用 OLE DB 來源。 您無法使用 Excel 來源，從 Excel 2007 資料來源載入資料。 如需詳細資訊，請參閱 [設定 OLE DB 連接管理員](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)。  
>   
>  若要從使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2003 或更早版本的資料來源載入資料，請使用 Excel 來源。 如需詳細資訊，請參閱 [Excel 來源編輯器 &#40;連接管理員頁面&#41;](../../integration-services/data-flow/excel-source-editor-connection-manager-page.md)。  
  
> [!NOTE]  
>  在 OLE DB 來源編輯器中無法使用 OLE DB 來源的 **CommandTimeout** 屬性，但可使用進階編輯器來設定這個屬性。 如需這個屬性的詳細資訊，請參閱 [OLE DB 自訂屬性](../../integration-services/data-flow/ole-db-custom-properties.md)的＜Excel 來源＞一節。  
  
### <a name="open-the-ole-db-source-editor-connection-manager-page"></a>開啟 OLE DB 來源編輯器 (連線管理員頁面)  
  
1.  將 OLE DB 來源加入 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝 (於 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中)。  
  
2.  以滑鼠右鍵按一下來源元件，然後按一下 [編輯]。  
  
3.  按一下 [連接管理員]。  
  
### <a name="static-options"></a>靜態選項  
 **[無快取]**  
 從清單中選取現有的連線管理員，或按一下 [新增] 來建立新的連線。  
  
 **新增**  
 使用 [設定 OLE DB 連線管理員] 對話方塊建立新的連線管理員。  
  
 **資料存取模式**  
 從來源中指定選取資料的方法。  
  
|選項|描述|  
|------------|-----------------|  
|資料表或檢視|從 OLE DB 資料來源中的資料表或檢視擷取資料。|  
|資料表名稱或檢視名稱變數|請在變數中指定資料表或檢視名稱。<br /><br /> **相關資訊︰**[在封裝中使用變數](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|SQL (命令)|使用 SQL 查詢從 OLE DB 資料來源中擷取資料。|  
|來自變數的 SQL 命令|在變數中指定 SQL 查詢文字。|  
  
 **預覽**  
 使用 [資料檢視] 對話方塊來預覽結果。 [預覽] 最多可顯示 200 個資料列。  
  
> [!NOTE]  
>  在預覽資料時，具有 CLR 使用者定義型別的資料行不會包含資料。 而會顯示 \<數值太大而無法顯示> 或 System.Byte[]。 使用 SQL OLE DB 提供者存取資料來源時會顯示前者，而使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 提供者時會顯示後者。  
  
### <a name="data-access-mode-dynamic-options"></a>資料存取模式動態選項  
  
#### <a name="data-access-mode--table-or-view"></a>資料存取模式 = 資料表或檢視  
 **資料表或檢視的名稱**  
 從資料來源中可用的清單中選取資料表或檢視名稱。  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>資料存取模式 = 資料表名稱或檢視名稱變數  
 **變數名稱**  
 請選取包含資料表或檢視名稱的變數。  
  
#### <a name="data-access-mode--sql-command"></a>資料存取模式 = SQL 命令  
 **SQL 命令文字**  
 輸入 SQL 查詢文字，按一下 [建立查詢] 建立查詢，或按一下 [瀏覽] 找到包含查詢文字的檔案。  
  
 **參數**  
 如果您所輸入的參數化查詢使用 ? 做為查詢文字中的參數預留位置，請使用 **[設定查詢參數]** 對話方塊，將查詢輸入參數對應到封裝變數。  
  
 **建立查詢**  
 使用 [查詢產生器] 對話方塊，以視覺化的方式來建構 SQL 查詢。  
  
 **瀏覽**  
 使用 [開啟] 對話方塊來找出包含 SQL 查詢文字的檔案。  
  
 **剖析查詢**  
 請確認查詢文字的語法。  
  
#### <a name="data-access-mode--sql-command-from-variable"></a>資料存取模式 = 來自變數的 SQL 命令  
 **變數名稱**  
 選取包含 SQL 查詢文字的變數。  
  
## <a name="ole-db-source-editor-columns-page"></a>OLE DB 來源編輯器 (資料行頁面)
  使用 [OLE DB 來源編輯器] 對話方塊的 [資料行] 頁面，即可將輸出資料行對應至每個外部 (來源) 資料行。  
  
### <a name="options"></a>選項。  
 **可用的外部資料行**  
 在資料來源中檢視可用的外部資料行清單。 您無法使用此資料表來加入或刪除資料行。  
  
 **[外部資料行]**  
 依您在設定使用此來源之資料的元件時所見的順序來檢視外部 (來源) 資料行。 首先取消選取資料表中選取的資料行，然後依不同順序從清單中選取外部資料行，就可以變更此順序。  
  
 **輸出資料行**  
 為每個輸出資料行提供唯一的名稱。 預設值為選取的外部 (來源) 資料行的名稱；不過，您也可以選擇任何唯一的、描述性的名稱。 提供的名稱將顯示在  設計師內。  
  
## <a name="ole-db-source-editor-error-output-page"></a>OLE DB 來源編輯器 (錯誤輸出頁面)
  使用 [OLE DB 來源編輯器] 對話方塊的 [錯誤輸出] 頁面，以選取錯誤處理選項，並設定錯誤輸出資料行上的屬性。  
  
### <a name="options"></a>選項。  
 **輸入/輸出**  
 檢視資料來源的名稱。  
  
 **資料行**  
 檢視您在 [OLE DB 來源編輯器] 對話方塊的 [連接管理員] 頁面上所選取的外部 (來源) 資料行。  
  
 **錯誤**  
 指定錯誤發生時要採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **相關主題** [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **截斷**  
 指定截斷發生時要採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **說明**  
 檢視錯誤的描述。  
  
 **將這個值設定到選取的資料格**  
 指定發生錯誤或截斷時要對所有選取之資料格採取的動作：忽略失敗、重新導向資料列，或使元件失效。  
  
 **套用**  
 將錯誤處理選項套用至選取的資料格。  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB 目的地](../../integration-services/data-flow/ole-db-destination.md)   
 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)   
 [資料流程](../../integration-services/data-flow/data-flow.md)  
  
  
