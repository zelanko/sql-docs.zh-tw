---
title: "指定資料表複製或查詢 (SQL Server 匯入和匯出精靈) | Microsoft Docs"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.specifytablecopyorquery.f1
ms.assetid: 08aa7158-40e6-4ef3-84d3-1265a8ba194c
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 56babe19727ca9ac7e0f364f64c91716508f4dfc
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="specify-table-copy-or-query-sql-server-import-and-export-wizard"></a>指定資料表複製或查詢 (SQL Server 匯入和匯出精靈)
  在您提供有關資料目的地及其連接方式的資訊之後，[ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 顯示 [指定資料表複製或查詢] 。 在此頁面上，您可以選擇下列其中一個選項。
-   **從一個或多個資料表或檢視表複製資料**。 您想要從清單中選取資料表。
-   **撰寫查詢來指定要傳送的資料**。 您想要輸入或貼入 SQL 查詢文字。
    
> [!TIP]
> 如果您必須複製多個資料庫，或資料表和檢視以外的資料庫物件，請使用 [複製資料庫精靈]，而非 [匯入和匯出精靈]。 如需詳細資訊，請參閱 [使用複製資料庫精靈](../../relational-databases/databases/use-the-copy-database-wizard.md)。     
 
## <a name="screen-shot-of-the-specify-table-copy-or-query-page"></a>[指定資料表複製或查詢] 頁面的螢幕擷取畫面    
 下列螢幕擷取畫面顯示精靈的 [指定資料表複製或查詢]  頁面。    
    
 ![[匯入和匯出精靈] 的 [資料表複製或查詢] 頁面](../../integration-services/import-export-data/media/table-copy-or-query.png "[匯入和匯出精靈] 的 [資料表複製或查詢] 頁面")    
    
## <a name="specify-whether-to-copy-an-entire-table-or-write-a-query"></a>指定要複製整份資料表或撰寫查詢 
 **從一個或多個資料表或檢視表複製資料**    
 如果您要複製來源中的資料，但不要篩選或排序記錄，請選取此選項。   

當您選取 [從一個或多個資料表或檢視表複製資料] 時，即可從一個資料表或檢視複製至一個目的地資料表，或從多個資料表或檢視複製至多個目的地資料表。

 按一下 [下一步] 之後，請在 [選取來源資料表和檢視表]  頁面上選取要複製的資料表。 如需詳細資訊，請參閱 [選取來源資料表和檢視表](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)。   
    
 **撰寫查詢來指定要傳送的資料**    
 如果您想要先篩選或排序來源資料，再將它複製至目的地，請選取此選項。    
    
當您選取 [寫入查詢來指定要傳送的資料] 時，只能將一個查詢的結果複製到一個目的地資料表。  

按一下 [下一步] 之後，請提供 SQL 陳述式來指定資料行，並在 [提供來源查詢]  對話方塊中選取資料列。 如需詳細資訊，請參閱 [提供來源查詢](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md)。   
    
## <a name="why-isnt-the-copy-option-available"></a>為何無法使用 [複製] 選項？    
 當精靈使用 **資料提供者連接您的資料來源時，可能會無法使用 [從一個或多個資料表或檢視表複製資料]**[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 選項。 這發生於當精靈的資料提供者資訊不足，而無法向資料來源要求資料表和檢視表清單時。 
 
只要您知道想要匯出之資料表的名稱，則仍然可以使用 [Write a query] (撰寫查詢) 選項，即使通常不會撰寫 SQL 查詢也是一樣。 在您按一下 [下一步] 後看到的 [提供來源查詢] 對話方塊中，將查詢輸入為 `SELECT * FROM <name of table>`。 如果資料表的名稱包含空格或其他特殊字元，則請使用方括弧括住名稱：`SELECT * FROM [<name of table>]`。

### <a name="more-info"></a>其他資訊
 [從一個或多個資料表或檢視表複製資料]  選項僅適用於在 ProviderDescriptors.xml 檔案中具有 ProviderDescription 區段的提供者。 (此檔案預設位於 \<磁碟機>:\Program Files\Microsoft SQL Server\130\DTS\ProviderDescriptors)。此檔案中的每個 ProviderDescription 區段都會包含從對應提供者擷取中繼資料所需的資訊。    
    
 依預設，只有針對下列清單中的提供者，ProviderDescriptors.xml 檔案才會包含 ProviderDescription 區段。    
    
-   .Net Framework Data Provider for SQL Server (System.Data.SqlClient)    
    
-   .Net Framework Data Provider for Oracle (System.Data.OracleClient)    
    
-   .Net Framework Data Provider for ODBC (System.Data.Odbc)    
    
-    System.Data.OleDb (適用於所有 OLE DB 提供者)    
    
-   Microsoft Host Integration Server 所安裝的 Microsoft Provider for DB2 (Microsoft.HostIntegration.MsDb2Client.MsDb2Connection)    
    
 協力廠商開發人員可以讓 [從一個或多個資料表或檢視表複製資料 ]  選項可供其提供者使用，方法是將 ProviderDescriptor 區段加入 ProviderDescriptors.xml 檔案中。 若要檢閱 ProviderDescriptor 區段的需求，請參閱 ProviderDescriptors.xsd 結構描述檔案 (依預設，其與 ProviderDescriptors.xml 檔案位於相同的資料夾中)。    
    
## <a name="whats-next"></a>下一步    
 在指定要複製整個資料表還是提供查詢之後，下一個頁面取決於您在此頁面上選擇的選項以及您資料的目的地。    
    
-   如果您選取 [從一個或多個資料表或檢視表複製資料] ，則針對大部分的目的地，下一個頁面是 [選取來源資料表和檢視表] 。 在此頁面上，您可以選取現有的資料表和檢視，以從資料來源複製到目的地。 如需詳細資訊，請參閱 [選取來源資料表和檢視表](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)。    
    
-   如果您選取 [從一個或多個資料表或檢視表複製資料]  ，而且目的地是一般檔案，則下一個頁面是 [設定一般檔案目的地] 。 在此頁面上，您可以指定目的地一般檔案的格式化選項。 (然後，在您設定一般檔案之後，下一個頁面是 [選取來源資料表和檢視表])。如需詳細資訊，請參閱[設定一般檔案目的地](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)。    
    
-   如果您選取 [撰寫查詢來指定要傳送的資料]，則下一個頁面是 [提供來源查詢]。 在此頁面上，您可以撰寫和測試 SQL 陳述式，以選取要從資料來源複製到目的地的資料。 (然後，提供查詢之後，下一個頁面是 [選取來源資料表和檢視表])。如需詳細資訊，請參閱[提供來源查詢](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md)。

## <a name="see-also"></a>另請參閱
[透過匯入和匯出精靈的簡單範例開始使用](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


