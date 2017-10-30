---
title: "開始使用這個簡單的範例，匯入和匯出精靈 |Microsoft 文件"
ms.custom: 
ms.date: 02/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: ea3db39b-698b-4a74-8eb8-21dc7252dc1a
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 59c7e1cc3c31f77652acb21d375e1294bdc93397
ms.openlocfilehash: 9eee58be471d8b39b051c1343f9eb26a2960b6d6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="get-started-with-this-simple-example-of-the-import-and-export-wizard"></a>開始使用 「 匯入和匯出精靈的這個簡單的範例
了解預期中的 SQL Server 匯入和匯出精靈 」 會帶您逐步完成常見的案例-從 Excel 試算表匯入資料到 SQL Server 資料庫。 即使您打算使用不同的來源和不同的目的，本主題說明您大部分的您需要了解執行精靈。

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>必要條件-是安裝在電腦上的精靈嗎？
如果您想要執行精靈，但電腦上尚未安裝 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則可以安裝 SQL Server Data Tools (SSDT) 來安裝 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈]。 如需詳細資訊，請參閱 [下載 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。

## <a name="heres-the-excel-source-data-for-this-example"></a>以下是此範例的 Excel 來源資料
以下是您要複製的小型的兩個資料行資料表 WizardWalkthrough 工作表 WizardWalkthrough.xlsx Excel 活頁簿中的來源資料。

![Excel 來源資料](../../integration-services/import-export-data/media/excel-source-data.jpg)

## <a name="heres-the-sql-server-destination-database-for-this-example"></a>以下是此範例中的 SQL Server 目的地資料庫
以下 （在 SQL Server Management Studio) 是要複製的來源資料的 SQL Server 目的地資料庫。 目的地資料表不存在-您要讓精靈為您建立資料表。

![SQL Server 目的地資料庫](../../integration-services/import-export-data/media/sql-server-destination-database.jpg)

## <a name="step-1---start-the-wizard"></a>步驟 1-啟動精靈
您啟動精靈，從 [開始] 功能表上的 Microsoft SQL Server 2016 群組。

![啟動精靈](../../integration-services/import-export-data/media/start-wizard.jpg)

> [!NOTE]
> 例如，您選擇 32 位元精靈，因為您已安裝 Microsoft Office 32 位元版本。 如此一來，您必須使用 32 位元資料提供者連接到 Excel。 許多其他資料來源，您通常可以選擇 64 位元精靈。
>
> 若要使用 64 位元版本的 SQL Server 匯入和匯出精靈，您必須安裝 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位元應用程式，並只安裝 32 位元檔案，包括 32 位元版本的精靈。

如需詳細資訊，請參閱 [啟動 SQL Server 匯入和匯出精靈](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)。

## <a name="step-2---view-the-welcome-page"></a>步驟 2-歡迎使用 頁面檢視
在精靈的第一頁**褖畫惎**頁面。 

您可能不想要看到此頁面，一次，因此請繼續並按一下**不要的顯示此開始頁面再次**。

![歡迎使用精靈](../../integration-services/import-export-data/media/welcome-to-the-wizard.jpg)

## <a name="step-3---pick-excel-as-your-data-source"></a>步驟 3-挑選 Excel 做為資料來源
在下一個頁面上，**選擇資料來源**，您可以挑選 Microsoft Excel 做為資料來源。 然後您瀏覽至選取 Excel 檔案。 最後，您會指定您用來建立檔案的 Excel 版本。

![選擇 Excel 資料來源](../../integration-services/import-export-data/media/choose-the-excel-data-source.jpg)

如需連接至 Excel 的詳細資訊，請參閱[連接到 Excel 資料來源](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)。 如需此頁面在精靈的詳細資訊，請參閱[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)。

## <a name="step-4---pick-sql-server-as-your-destination"></a>步驟 4-挑選做為目的地的 SQL Server
在下一個頁面上，**選擇目的地**，您挑選為您的目的地所挑選其中一個資料提供者清單中，連接至 SQL Server 的 Microsoft SQL Server。 在此範例中，您挑選**.Net Framework Data Provider for SQL Server**。

頁面會顯示一份提供者屬性。 其中有許多惡意的名稱和不熟悉的設定。 幸運的是，若要連接至企業中的任何資料庫，通常必須提供只有三組資訊。 您可以忽略其他設定的預設值。

|所需的資訊|.Net framework Data Provider for SQL Server 屬性|
|---|---|
|伺服器名稱|**資料來源**|
|驗證 （登入） 資訊|**整合式安全性**; 或**使用者識別碼**和**密碼**<br/>如果您想要在伺服器上看到資料庫的下拉式清單，您需要先提供有效的登入資訊。|
|資料庫名稱|**初始目錄**|

![選擇 SQL Server 目的地](../../integration-services/import-export-data/media/choose-the-sql-server-destination.jpg)

如需連接到 SQL Server 的詳細資訊，請參閱[連接到 SQL Server 資料來源](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)。 如需此頁面在精靈的詳細資訊，請參閱[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)。

## <a name="step-5---copy-a-table-instead-of-writing-a-query"></a>步驟 5-複製的資料表，而不是撰寫查詢
在下一個頁面上，**指定資料表複製或查詢**，您可以指定您要複製的來源資料的整個資料表。 您不想要選取要複製資料的 SQL 語言撰寫的查詢。

![指定要複製資料表](../../integration-services/import-export-data/media/specify-to-copy-a-table.jpg)

如需此頁面在精靈的詳細資訊，請參閱[指定資料表複製或查詢](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)。

## <a name="step-6---pick-the-table-to-copy"></a>步驟 6-選取要複製的資料表
在下一個頁面上，**選取來源資料表和檢視**，挑選您想要從資料來源複製的資料表。 然後您將每個所選的來源資料表對應至新的或現有的目的地資料表。

在此範例中，依預設精靈已對應**WizardWalkthrough$**中的工作表**來源**具有相同名稱的 SQL Server 目的地的新資料表的資料行。 （Excel 活頁簿僅包含單一工作表）。
-   貨幣符號 （$） 的來源資料表名稱表示 Excel 工作表。 （具名，遠距在 Excel 中被以其本身的名稱。）
-   爆炸目的地資料表圖示表示精靈正在建立新的目的地資料表。

![選取的資料表 （在之前重新命名）](../../integration-services/import-export-data/media/select-the-table-before-renaming.jpg)

您可能想要移除錢幣符號 （$） 的新目的地資料表名稱。

![選取的資料表 （重新命名之後）](../../integration-services/import-export-data/media/select-the-table-after-renaming.jpg)

如需此頁面在精靈的詳細資訊，請參閱[選取來源資料表和檢視](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)。

## <a name="optional-step-7---review-the-column-mappings"></a>選擇性的步驟 7-檢閱資料行對應
在遠行之前**選取來源資料表和檢視**頁面上，選擇性地按一下**編輯對應** 按鈕以開啟**資料行對應** 對話方塊。 這裡的**對應**資料表中，您會看到精靈要如何將來源工作表中的資料行對應至新的目的地資料表中的資料行。

![檢視資料行對應](../../integration-services/import-export-data/media/view-column-mappings.jpg)

如需此頁面在精靈的詳細資訊，請參閱[資料行對應](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。

## <a name="optional-step-8---review-the-create-table-statement"></a>選擇性的步驟 8-檢閱 CREATE TABLE 陳述式
雖然**資料行對應**對話方塊開啟時，選擇性地按一下**編輯 SQL**  按鈕以開啟**建立資料表 SQL 陳述式** 對話方塊。 您在這裡看到**CREATE TABLE**精靈以建立新的目的地資料表所產生的陳述式。 通常您不需要變更的陳述式。

![檢視 CREATE TABLE 陳述式](../../integration-services/import-export-data/media/view-create-table-statement.jpg)

如需此頁面在精靈的詳細資訊，請參閱[建立資料表 SQL 陳述式](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)。

## <a name="optional-step-9---preview-the-data-to-copy"></a>選擇性的步驟 9-預覽要複製資料
按一下之後**確定**關閉**建立資料表 SQL 陳述式**對話方塊方塊，然後按一下  **確定**  以關閉 **資料行對應**對話方塊中，您在上一步**選取來源資料表和檢視**頁面。 （選擇性） 按一下**預覽**按鈕可查看資料的範例，精靈將會進行複製。 在此範例中，它會尋找 [確定]。

![要複製預覽資料](../../integration-services/import-export-data/media/preview-data-to-copy.jpg)

如需此頁面在精靈的詳細資訊，請參閱[預覽資料](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)。

## <a name="step-10---yes-you-want-to-run-the-import-export-operation"></a>步驟 10-[是]，以您想要執行匯入匯出作業。
在下一個頁面上，**儲存和執行封裝**，您將**立即執行**複製資料，當您按一下啟用**完成**在下一個頁面。 您可以按一下 略過下一個頁面或者**完成**上**儲存和執行封裝**頁面。

![執行封裝](../../integration-services/import-export-data/media/run-the-package.jpg)

如需此頁面在精靈的詳細資訊，請參閱[儲存和執行封裝](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。

## <a name="step-11---finish-the-wizard-and-run-the-import-export-operation"></a>步驟 11-結束精靈，執行匯入匯出作業。
如果您按下**下一步**而不是**完成**上**儲存和執行封裝**頁面上，然後在下一個頁面上，**完成精靈**，您會看到精靈將要執行的摘要。 按一下**完成**執行匯入匯出作業。

![完成精靈](../../integration-services/import-export-data/media/complete-the-wizard.jpg)

如需此頁面在精靈的詳細資訊，請參閱[完成精靈](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)。

## <a name="step-12---review-what-the-wizard-did"></a>步驟 12-檢閱精靈的未
最終頁面上，查看在精靈完成每項工作，然後檢閱結果。 強調顯示的行會指示精靈成功地複製您的資料。 在完成 ！

![精靈成功](../../integration-services/import-export-data/media/the-wizard-succeeded.jpg)

如需此頁面在精靈的詳細資訊，請參閱[正在執行作業](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md)。

## <a name="heres-the-new-table-of-data-copied-to-sql-server"></a>以下是新的資料複製到 SQL Server 資料表
（在 SQL Server Management Studio) 您查看精靈建立 SQL Server 中的新目的地資料表。

![資料複製到 SQL Server](../../integration-services/import-export-data/media/data-copied-to-sql-server.jpg)

這裡 （一次在 SSMS) 中您會看到精靈複製到 SQL Server 的資料。

![資料複製到 SQL Server 2](../../integration-services/import-export-data/media/data-copied-to-sql-server-2.jpg)

## <a name="learn-more"></a>深入了解  
深入了解精靈如何運作。
-   **深入了解精靈。** 如果您要尋找精靈概觀，請參閱 [使用 SQL Server 匯入及匯出精靈匯入和匯出資料](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。

-   **深入了解精靈中的步驟。** 如果您想要尋求精靈中的步驟的相關資訊，從這裡的清單中選取您要的頁面[的 SQL Server 匯入和匯出精靈 」 中的步驟](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md)。 也是在精靈的每一頁的文件的個別頁面。

-   **了解如何連接到資料來源和目的地。** 如果您要尋找如何連接到您資料的相關資訊，從這裡的清單中選取您要的頁面[連接到資料來源的 SQL Server 匯入和匯出精靈](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md)。 沒有針對數個常用的資料來源的每個文件的個別頁面。



