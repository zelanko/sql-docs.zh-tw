---
title: 開始使用這個匯入和匯出精靈的簡單範例 | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: get-started-article
ms.assetid: ea3db39b-698b-4a74-8eb8-21dc7252dc1a
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 65a35f21680352f663e0d65a9f4404cdd8ea3e16
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35403220"
---
# <a name="get-started-with-this-simple-example-of-the-import-and-export-wizard"></a>開始使用這個匯入和匯出精靈的簡單範例
逐步執行將資料從 Excel 試算表匯入至 SQL Server 資料庫的這個常見案例，以了解 [SQL Server 匯入和匯出精靈] 中的預期作業。 即使您要使用不同的來源和不同的目的地，本主題還是會示範您執行精靈時所需知道的大部分內容。

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>必要條件 - 電腦上已安裝精靈嗎？
如果您想要執行精靈，但電腦上尚未安裝 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則可以安裝 SQL Server Data Tools (SSDT) 來安裝 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈]。 如需詳細資訊，請參閱 [下載 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。

## <a name="heres-the-excel-source-data-for-this-example"></a>以下是此範例的 Excel 來源資料
以下是您要複製的來源資料：WizardWalkthrough.xlsx Excel 活頁簿的 WizardWalkthrough 工作表中的小型兩個資料行資料表。

![Excel 來源資料](../../integration-services/import-export-data/media/excel-source-data.jpg)

## <a name="heres-the-sql-server-destination-database-for-this-example"></a>以下是此範例的 SQL Server 目的地資料庫
這裡 (在 SQL Server Management Studio 中) 是您要將來源資料複製至其中的 SQL Server 目的地資料庫。 目的地資料表不存在 - 您要讓精靈為您建立資料表。

![SQL Server 目的地資料庫](../../integration-services/import-export-data/media/sql-server-destination-database.jpg)

## <a name="step-1---start-the-wizard"></a>步驟 1 - 啟動精靈
您可以從 Windows [開始] 功能表的 Microsoft SQL Server 2016 群組中啟動精靈。

![啟動精靈](../../integration-services/import-export-data/media/start-wizard.jpg)

> [!NOTE]
> 在此範例中，因為您已安裝 32 位元版本的 Microsoft Office，所以會挑選 32 位元精靈。 因此，您必須使用 32 位元資料提供者連線至 Excel。 針對許多其他資料來源，您通常可以挑選 64 位元精靈。
>
> 若要使用 64 位元版本的 [SQL Server 匯入和匯出精靈]，您必須安裝 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位元應用程式，而且只會安裝 32 位元檔案 (包含 32 位元版本的精靈)。

如需詳細資訊，請參閱 [啟動 SQL Server 匯入和匯出精靈](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)。

## <a name="step-2---view-the-welcome-page"></a>步驟 2 - 檢視歡迎頁面
精靈的第一頁是 [歡迎] 頁面。 

您可能不想再看到此頁面，因此請繼續並按一下 [不要再顯示此開始頁面]。

![歡迎使用精靈](../../integration-services/import-export-data/media/welcome-to-the-wizard.jpg)

## <a name="step-3---pick-excel-as-your-data-source"></a>步驟 3 - 挑選 Excel 作為資料來源
在下一個 [選擇資料來源] 頁面上，您可以挑選 Microsoft Excel 作為資料來源。 您接著可以瀏覽以挑選 Excel 檔案。 最後，您會指定用來建立檔案的 Excel 版本。

> [!IMPORTANT]
> 如需連接至 Excel 檔案，以及將資料從 Excel 檔案載入或載入至 Excel 檔案的限制與已知問題的詳細資訊，請參閱[使用 SQL Server Integration Services (SSIS) 將資料從 Excel 載入或載入至 Excel](../load-data-to-from-excel-with-ssis.md)。

![選擇 Excel 資料來源](../../integration-services/import-export-data/media/choose-the-excel-data-source.jpg)

如需精靈之這個頁面的詳細資訊，請參閱[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)。

## <a name="step-4---pick-sql-server-as-your-destination"></a>步驟 4 - 挑選 SQL Server 作為目的地
在下一個 [選擇目的地] 頁面上，您可以挑選清單中連線至 SQL Server 的其中一個資料提供者，以挑選 Microsoft SQL Server 作為目的地。 在此範例中，您挑選 **.Net Framework Data Provider for SQL Server**。

頁面會顯示一份提供者屬性清單。 其中有許多是不易記的名稱和不熟悉的設定。 幸運的是，若要連線至任何企業資料庫，您通常只需要提供三項資訊。 您可以忽略其他設定的預設值。

|必要資訊|.Net Framework Data Provider for SQL Server 屬性|
|---|---|
|伺服器名稱|**資料來源**|
|驗證 (登入) 資訊|[整合式安全性]；或 [使用者識別碼] 和 [密碼]<br/>如果您想要在伺服器上看到資料庫下拉式清單，則需要先提供有效的登入資訊。|
|資料庫名稱|**初始目錄**|

![選擇 SQL Server 目的地](../../integration-services/import-export-data/media/choose-the-sql-server-destination.jpg)

如需連線至 SQL Server 的詳細資訊，請參閱[連線至 SQL Server 資料來源](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)。 如需精靈之這個頁面的詳細資訊，請參閱[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)。

## <a name="step-5---copy-a-table-instead-of-writing-a-query"></a>步驟 5 - 複製資料表，而非撰寫查詢
在下一個 [指定資料表複製或查詢] 頁面上，您可以指定要複製整個來源資料表。 您不想要使用 SQL 語言來撰寫查詢，以選取要複製的資料。

![指定以複製資料表](../../integration-services/import-export-data/media/specify-to-copy-a-table.jpg)

如需精靈之這個頁面的詳細資訊，請參閱[指定資料表複製或查詢](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)。

## <a name="step-6---pick-the-table-to-copy"></a>步驟 6 - 挑選要複製的資料表
在下一個 [選取來源資料表和檢視] 頁面上，您可以挑選想要從資料來源複製的資料表。 接著，您可以將每個選取的來源資料表對應至新的或現有目的地資料表。

在此範例中，精靈預設已將 [來源] 資料行中的 **WizardWalkthrough$** 工作表對應至 SQL Server 目的地上同名的新資料表  (Excel 活頁簿只包含單一工作表)。
-   來源資料表名稱上的貨幣符號 ($) 指出是 Excel 工作表  (Excel 中的具名範圍是單獨以其名稱呈現)。
-   目的地資料表圖示上的爆炸指出精靈即將建立新的目的地資料表。

![選取資料表 (重新命名之前)](../../integration-services/import-export-data/media/select-the-table-before-renaming.jpg)

您可能想要移除新目的地資料表名稱中的錢幣符號 ($)。

![選取資料表 (重新命名之後)](../../integration-services/import-export-data/media/select-the-table-after-renaming.jpg)

如需精靈之這個頁面的詳細資訊，請參閱[選取來源資料表和檢視](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)。

## <a name="optional-step-7---review-the-column-mappings"></a>選擇性步驟 7 - 檢閱資料行對應
在您離開 [選取來源資料表和檢視] 頁面之前，請選擇性地按一下 [編輯對應] 按鈕以開啟 [資料行對應] 對話方塊。 在這裡，於 [對應] 資料表中，您會看到精靈要如何將來源工作表中的資料行對應至新目的地資料表中的資料行。

![檢視資料行對應](../../integration-services/import-export-data/media/view-column-mappings.jpg)

如需精靈之這個頁面的詳細資訊，請參閱[資料行對應](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。

## <a name="optional-step-8---review-the-create-table-statement"></a>選擇性步驟 8 - 檢閱 CREATE TABLE 陳述式
開啟 [資料行對應] 對話方塊時，選擇性地按一下 [編輯 SQL ] 按鈕開啟 [建立資料表的 SQL 陳述式] 對話方塊。 您可以在這裡看到精靈所產生的 **CREATE TABLE** 陳述式，以建立新的目的地資料表。 您通常不需要變更陳述式。

![檢視 CREATE TABLE 陳述式](../../integration-services/import-export-data/media/view-create-table-statement.jpg)

如需精靈之這個頁面的詳細資訊，請參閱[建立資料表的 SQL 陳述式](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)。

## <a name="optional-step-9---preview-the-data-to-copy"></a>選擇性步驟 9 - 預覽要複製的資料
在您按一下 [確定] 關閉 [建立資料表的 SQL 陳述式] 對話方塊，然後按一下 [確定] 關閉 [資料行對應] 對話方塊之後，就會回到 [選取來源資料表和檢視] 頁面。 選擇性地按一下 [預覽] 按鈕以查看精靈即將複製的資料範例。 在此範例中，一切正常。

![要複製的預覽資料](../../integration-services/import-export-data/media/preview-data-to-copy.jpg)

如需精靈之這個頁面的詳細資訊，請參閱[預覽資料](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)。

## <a name="step-10---yes-you-want-to-run-the-import-export-operation"></a>步驟 10 - 是，您想要執行匯入/匯出作業
在下一個 [儲存並執行套件] 頁面上，您可以啟用 [立即執行] 在按下一個頁面上的 [完成] 時盡快複製資料。 或者，您可以按一下 [儲存並執行套件] 頁面上的 [完成]，跳過下一個頁面。

![執行套件](../../integration-services/import-export-data/media/run-the-package.jpg)

如需精靈之這個頁面的詳細資訊，請參閱[儲存並執行套件](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。

## <a name="step-11---finish-the-wizard-and-run-the-import-export-operation"></a>步驟 11 - 完成精靈並執行匯入/匯出作業
如果您按一下 [下一步]，而不是 [儲存並執行套件] 頁面上的 [完成]，則在下一個 [完成精靈] 頁面上，您會看到精靈將執行作業的摘要。 按一下 [完成] 執行匯入/匯出作業。

![完成精靈](../../integration-services/import-export-data/media/complete-the-wizard.jpg)

如需精靈之這個頁面的詳細資訊，請參閱[完成精靈](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)。

## <a name="step-12---review-what-the-wizard-did"></a>步驟 12 - 檢閱精靈已執行的作業
在最後一個頁面上，於精靈完成每項工作時查看，然後檢閱結果。 強調顯示的行指出精靈已成功地複製您的資料。 您已完成！

![精靈成功](../../integration-services/import-export-data/media/the-wizard-succeeded.jpg)

如需精靈之這個頁面的詳細資訊，請參閱[執行作業](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md)。

## <a name="heres-the-new-table-of-data-copied-to-sql-server"></a>以下是複製至 SQL Server 的新資料表
您可以在這裡 (於 SQL Server Management Studio 中) 看到精靈於 SQL Server 中所建立的新目的地資料表。

![要複製至 SQL Server 的資料](../../integration-services/import-export-data/media/data-copied-to-sql-server.jpg)

您可以在這裡 (同樣於 SSMS 中) 看到精靈已複製至 SQL Server 的資料。

![要複製至 SQL Server 2 的資料](../../integration-services/import-export-data/media/data-copied-to-sql-server-2.jpg)

## <a name="learn-more"></a>深入了解  
深入了解精靈運作方式。
-   **深入了解此精靈。** 如果您要尋找精靈概觀，請參閱 [使用 SQL Server 匯入及匯出精靈匯入和匯出資料](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。

-   **了解此精靈的步驟。** 如果您要尋找精靈中各步驟的資訊，請從這裡的清單中選取您想要的頁面 - [SQL Server 匯入和匯出精靈中的步驟](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md)。 精靈的每個頁面也都會有個別文件頁面。

-   **了解如何連線至資料來源和目的地。** 如果您要尋找如何連線至資料的資訊，請從這裡的清單中選取您想要的頁面 - [使用 SQL Server 匯入和匯出精靈連線至資料來源](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md)。 數個常用資料來源都各有個別文件頁面。

-   **深入了解將資料從 Excel 載入或載入至 Excel。** 如果您在尋找連接至 Excel 檔案，以及將資料從 Excel 檔案載入或載入至 Excel 檔案的限制與已知問題的詳細資訊，請參閱[使用 SQL Server Integration Services (SSIS) 將資料從 Excel 載入或載入至 Excel](../load-data-to-from-excel-with-ssis.md)。