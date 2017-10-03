---
title: "SQL Server 匯入和匯出精靈中的步驟 |Microsoft 文件"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 816fb1bd-7bb9-450d-ad65-e4c2d02eaff8
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 22d1f4b78fadab6d7b6659104b54a564f11da308
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="steps-in-the-sql-server-import-and-export-wizard"></a>SQL Server 匯入和匯出精靈中的步驟
本主題描述匯入和匯出資料的 SQL Server 匯入和匯出精靈的步驟的順序。 它也包含描述每個頁面的文件或您在精靈中看到的對話方塊的各個頁面的連結。

本主題只說明**步驟**精靈中。 如果您想要尋求其他項目，請參閱[相關的工作和內容](#related)。

## <a name="steps-for-importing-and-exporting-data"></a>匯入和匯出資料的步驟  
 下表列出匯入和匯出資料的步驟以及對應的精靈頁面。 根據您在精靈中選取的選項，您通常沒有看到所有頁面。  

快速瀏覽數個您在一般的工作階段中看到的畫面，看看這個簡單的端對端範例在單一頁面-[開始匯入和匯出精靈 」 的這個簡單的範例使用](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)。

|步驟|精靈頁面|  
|----------|------------------|  
|**歡迎使用**<br />您不需要在此頁面上採取任何動作。|[歡迎使用 SQL Server 匯入和匯出精靈](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)|  
|**挑選資料來源**。|[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)|  
|**選取資料目的地**。|[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)|  
|**設定目的地**。 （選擇性步驟）<br /><br /> -   建立新的目的地資料庫。<br />-   如果要將資料複製到文字檔案，請設定其他設定。|[建立資料庫](../../integration-services/import-export-data/create-database-sql-server-import-and-export-wizard.md)<br /><br />[設定一般檔案目的地](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)|  
|**指定您要複製。**|[指定資料表複製或查詢](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)<br /><br />[選取來源資料表和檢視表](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)<br /><br />[提供來源查詢](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md)|  
|**設定的複製作業**。 （選擇性步驟）<br /><br /> -   建立新的目的地資料表。<br />-決定該怎麼辦精靈並不知道如何將您選取的目的地與來源之間的資料類型對應。<br />-   檢閱來源與目的地之間的資料行對應。<br />-   處理來源與目的地之間的資料類型轉換問題。<br />-   預覽要複製的資料。|[建立資料表的 SQL 陳述式](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)<br /><br />[轉換類型但不檢查轉換](../../integration-services/import-export-data/convert-types-without-conversion-checking-sql-server-import-and-export-wizard.md)<br /><br />[資料行對應](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)<br /><br />[檢閱資料類型對應](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)<br /><br />[資料行轉換詳細資料對話方塊](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md)<br /><br />[預覽資料對話方塊](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)|  
|**將資料複製。**<br /><br /> （選擇性） 將您的設定儲存為 SQL Server Integration Services (SSIS) 封裝。|[儲存並執行封裝](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)<br /><br />[儲存 SSIS 套件](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)<br /><br />[完成精靈](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)<br /><br />[執行作業](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md)|  

> [!TIP]
> 在精靈的任何頁面或對話方塊中點選 F1 鍵，以查看目前頁面的文件。

## <a name="related"></a>相關的工作和內容  
以下是一些基本的工作。
-   **在精靈的運作方式的簡單的範例，請參閱。**

    -   **如果您想要查看螢幕擷取畫面。** 在單一頁面-看看這個簡單的端對端範例[開始匯入和匯出精靈 」 的這個簡單的範例使用](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)。

    -   **如果您想要觀看影片。** 觀賞此四分鐘的影片與 YouTube 示範精靈和清楚地說明只是如何將資料匯出至 Excel-[使用 SQL Server 匯入和匯出精靈 來匯出至 Excel](https://go.microsoft.com/fwlink/?linkid=829049)。

-   **深入了解精靈如何運作。**

    -   **深入了解精靈。** 如果您要尋找精靈概觀，請參閱 [使用 SQL Server 匯入及匯出精靈匯入和匯出資料](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。

    -   **了解如何連接到資料來源和目的地。** 如果您要尋找如何連接到您資料的相關資訊，從這裡的清單中選取您要的頁面[連接到資料來源的 SQL Server 匯入和匯出精靈](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md)。 沒有針對數個常用的資料來源的每個文件的個別頁面。 

-   **啟動精靈。** 如果您準備好要執行精靈，且只是想要知道其啟動方式，請參閱[啟動 SQL Server 匯入和匯出精靈](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)。

-     **取得精靈。** 如果您想要執行精靈，但電腦上尚未安裝 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則可以安裝 SQL Server Data Tools (SSDT) 來安裝 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈]。 如需詳細資訊，請參閱 [下載 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。



