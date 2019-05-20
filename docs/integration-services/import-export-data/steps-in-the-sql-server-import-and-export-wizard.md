---
title: SQL Server 匯入和匯出精靈中的步驟 | Microsoft Docs
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 816fb1bd-7bb9-450d-ad65-e4c2d02eaff8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dafe47a0a136c7ab5640fc667b46cc496cfdbcb2
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65723696"
---
# <a name="steps-in-the-sql-server-import-and-export-wizard"></a>SQL Server 匯入和匯出精靈中的步驟

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


本主題描述使用 [SQL Server 匯入和匯出精靈] 匯入和匯出資料的一系列步驟。 它也會包含個別文件頁面的連結，而這些頁面描述您在精靈中看到的每個頁面或對話方塊。

本主題僅描述精靈中的**步驟**。 如需其他資訊，請參閱[相關的工作及內容](#related)。

## <a name="steps-for-importing-and-exporting-data"></a>匯入和匯出資料的步驟  
 下表列出匯入和匯出資料的步驟以及對應的精靈頁面。 根據您在精靈中選取的選項，您一般看不到所有這些頁面。  

若要快速查看您在一般工作階段中看到的數個畫面，請在單一頁面查看此簡單端對端範例 - [透過匯入和匯出精靈的簡單範例開始使用](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)。

|步驟|精靈頁面|  
|----------|------------------|  
|**歡迎使用**<br />您不需要在此頁面上採取任何動作。|[歡迎使用 SQL Server 匯入和匯出精靈](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)|  
|**挑選資料來源**。|[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)|  
|**選取資料目的地**。|[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)|  
|**設定目的地**. (選擇性步驟)<br /><br /> -   建立新的目的地資料庫。<br />-   如果要將資料複製到文字檔案，請設定其他設定。|[建立資料庫](../../integration-services/import-export-data/create-database-sql-server-import-and-export-wizard.md)<br /><br />[設定一般檔案目的地](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)|  
|**指定要複製的內容。**|[指定資料表複製或查詢](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)<br /><br />[選取來源資料表和檢視](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)<br /><br />[提供來源查詢](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md)|  
|**設定複製作業**. (選擇性步驟)<br /><br /> -   建立新的目的地資料表。<br />-   如果精靈不知道如何對應您選取的來源與目的地之間的資料類型，決定因應措施。<br />-   檢閱來源與目的地之間的資料行對應。<br />-   處理來源與目的地之間的資料類型轉換問題。<br />-   預覽要複製的資料。|[建立資料表 SQL 陳述式](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)<br /><br />[轉換類型但不檢查轉換](../../integration-services/import-export-data/convert-types-without-conversion-checking-sql-server-import-and-export-wizard.md)<br /><br />[資料行對應](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)<br /><br />[檢閱資料類型對應](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)<br /><br />[資料行轉換詳細資訊對話方塊](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md)<br /><br />[預覽資料對話方塊](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)|  
|**複製資料。**<br /><br /> 選擇性地將您的設定儲存為 SQL Server Integration Services (SSIS) 套件。|[儲存並執行套件](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)<br /><br />[儲存 SSIS 套件](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)<br /><br />[完成精靈](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)<br /><br />[執行作業](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md)|  

> [!TIP]
> 在精靈的任何頁面或對話方塊中點選 F1 鍵，以查看目前頁面的文件。

## <a name="related"></a> 相關的工作及內容  
以下是一些其他基本工作。
-   **請參閱精靈運作方式的簡單範例**。

    -   **若要檢視螢幕擷取畫面。** 您可以參考單一頁面上顯示的簡單端對端範例，[從 [匯入及匯出精靈] 的簡單範例開始著手](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)。

    -   **若要觀看影片。** YouTube 上備有此精靈的示範影片，片長四分鐘。影片中將專門針對如何[使用 SQL Server 的 [匯入及匯出精靈]，將資料匯出至 Excel ](https://go.microsoft.com/fwlink/?linkid=829049)清楚地說明。

-   **深入了解此精靈的運作方式。**

    -   **深入了解此精靈。** 如果您要尋找精靈概觀，請參閱 [使用 SQL Server 匯入及匯出精靈匯入和匯出資料](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。

    -   **了解如何連線至資料來源和目的地。** 如果您要尋找如何連線至資料的資訊，請從這裡的清單中選取您想要的頁面 - [使用 SQL Server 匯入和匯出精靈連線至資料來源](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md)。 數個常用資料來源都各有個別文件頁面。 

-   **啟動此精靈** 如果您準備好要執行精靈，且只是想要知道其啟動方式，請參閱[啟動 SQL Server 匯入和匯出精靈](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)。

-     **取得精靈。** 如果您想要執行精靈，但電腦上尚未安裝 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則可以安裝 SQL Server Data Tools (SSDT) 來安裝 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈]。 如需詳細資訊，請參閱 [下載 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。


