---
title: OLE DB 來源 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbsource.f1
helpviewer_keywords:
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: f87cc5f6-b078-40f3-9d87-7a65e13e4c86
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1b1d37bba3216a22d732c5562108db51925d37bf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48120575"
---
# <a name="ole-db-source"></a>OLE DB 來源
  OLE DB 來源會使用資料庫資料表、檢視或 SQL 命令，從各種 OLE DB 相容的關聯式資料庫中擷取資料。 例如，OLE DB 來源可從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的資料表中擷取資料。  
  
 OLE DB 來源提供四種不同的資料存取模式用來擷取資料：  
  
-   資料表或檢視。  
  
-   在變數中指定的資料表或檢視。  
  
-   SQL 陳述式的結果。 查詢可以是參數化查詢。  
  
-   儲存在變數中之 SQL 陳述式的結果。  
  
> [!NOTE]  
>  當您使用 SQL 陳述式呼叫從暫存資料表傳回結果的預存程序時，請使用 WITH RESULT SETS 選項定義結果集的中繼資料。  
  
 如果使用參數化查詢，您可以將變數對應到參數，以指定 SQL 陳述式中個別參數的值。  
  
 此來源使用 OLE DB 連接管理員連接到資料來源，且連接管理員會指定要使用的 OLE DB 提供者。 如需相關資訊，請參閱 [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md)。  
  
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
  
 預存程序需要有變數 `@StartProductID` 和 `@CheckDate`，才能提供參數值。 參數出現在 [對應] 清單中的順序並無任何影響。 唯一的需求是參數名稱必須符合預存程序中的變數名稱，包括 \@ 符號。  
  
### <a name="mapping-parameters-to-variables"></a>將參數對應至變數  
 參數會對應到在執行階段中提供參數值的變數。 這些變數通常是使用者自訂變數，不過您也可以使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的系統變數。 如果您使用的是使用者自訂變數，請務必將資料類型設定為與對應參數所參考之資料行資料類型相容的類型。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../integration-services-ssis-variables.md)。  
  
## <a name="troubleshooting-the-ole-db-source"></a>疑難排解 OLE DB 來源  
 您可以記錄 OLE DB 來源對外部資料提供者所執行的呼叫。 您可以使用這項記錄功能，疑難排解 OLE DB 來源執行的從外部資料來源載入資料的作業。 若要記錄 OLE DB 來源對外部資料提供者執行的呼叫，請啟用封裝記錄，然後在封裝層級選取 [診斷] 事件。 如需詳細資訊，請參閱[封裝執行的疑難排解工具](../troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="configuring-the-ole-db-source"></a>設定 OLE DB 來源  
 您可以程式設計方式或透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」設定屬性。  
  
 如需可在 [OLE DB 來源編輯器] 對話方塊中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [OLE DB 來源編輯器&#40;連線管理員頁面&#41;](../ole-db-source-editor-connection-manager-page.md)  
  
-   [OLE DB 來源編輯器&#40;資料行頁面&#41;](../ole-db-source-editor-columns-page.md)  
  
-   [OLE DB 來源編輯器&#40;錯誤輸出頁面&#41;](../ole-db-source-editor-error-output-page.md)  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](../common-properties.md)  
  
-   [OLE DB 自訂屬性](ole-db-custom-properties.md)  
  
## <a name="related-tasks"></a>相關工作  
  
-   [使用 OLE DB 來源來擷取資料](ole-db-source.md)  
  
-   [在資料流程元件中將查詢參數對應至變數](map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [設定資料流程元件的屬性](set-the-properties-of-a-data-flow-component.md)  
  
-   [排序合併和合併聯結轉換的資料](transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-content"></a>相關內容  
 social.technet.microsoft.com 上的 Wiki 文章： [SSIS with Oracle Connectors](http://go.microsoft.com/fwlink/?LinkId=220670)(SSIS 與 Oracle 連接器)。  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB 目的地](ole-db-destination.md)   
 [Integration Services &#40;SSIS&#41;變數](../integration-services-ssis-variables.md)   
 [資料流程](data-flow.md)  
  
  
