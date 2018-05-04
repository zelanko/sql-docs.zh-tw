---
title: 使用 SSIS 將資料從 Excel 載入或載入至 Excel | Microsoft Docs
ms.description: Describes how to import data from Excel or export data to Excel with SQL Server Integration Services (SSIS). Also describes prerequisites, known issues, and limitations.
ms.date: 04/10/2018
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: article
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8c31229aab550138805a912ffe40a33d08143205
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="load-data-from-or-to-excel-with-sql-server-integration-services-ssis"></a>使用 SQL Server Integration Services (SSIS) 將資料從 Excel 載入或載入至 Excel

本文描述如何使用 SQL Server Integration Services (SSIS) 從 Excel 匯入資料，或將資料匯出至 Excel。 本文也描述必要條件、限制和已知問題。

您可以藉由建立 SSIS 套件，並使用 Excel 連線管理員和 Excel 來源或 Excel 目的地，從 Excel 匯入資料，或將資料匯出至 Excel。 您也可以使用建立在 SSIS 上的 [SQL Server 匯入和匯出精靈]。

本文包含成功從 SSIS 使用 Excel，或要了解及針對常見問題進行疑難排解所需的三組資訊：
-   [您需要的檔案](#files-you-need)。
-   當您使用 Excel 載入或取出資料時，您必須提供的資訊。
    -   [指定 Excel](#specify-excel) 作為資料來源。
    -   提供 [Excel 檔案名稱和路徑](#excel-file)。
    -   選取 [Excel 版本](#excel-version)。
    -   指定是否在[第一個資料列包含資料行名稱](#first-row)。
    -   提供[包含資料的工作表或範圍](#sheets-ranges)。
-   已知問題和限制。
    -   [資料類型](#issues-types)的問題。
    -   [匯入](#issues-importing)的問題。
    -   [匯出](#issues-exporting)的問題。

## <a name="files-you-need"></a> 取得連線至 Excel 所需的檔案

您可能必須下載適用於 Excel 的連線元件，如果它們尚未安裝的話，然後才能從 Excel 匯入資料，或將資料匯出至 Excel。 預設不會安裝適用於 Excel 的連線元件。

在這裡下載適用於 Excel 的連線元件最新版本：[Microsoft Access Database Engine 2016 可轉散發套件](https://www.microsoft.com/download/details.aspx?id=54920)。
  
最新版的元件可以開啟舊版 Excel 所建立的檔案。

請確定下載 Access Database Engine 2016「可轉散發套件」，而非 Microsoft Access 2016 *Runtime*。

如果電腦已有 32 位元版的 Office，您就必須安裝 32 位元版的元件。 您也必須確定您在 32 位元模式中執行 SSIS 套件，或執行 [匯入和匯出精靈] 的 32 位元版本。

如果您有 Office 365 訂閱，可能會在執行安裝程式時看到一則錯誤訊息。 錯誤訊息指出您無法使用 Office 隨選即用元件並存安裝下載。 若要略過此錯誤訊息，請開啟 [命令提示字元] 視窗並執行使用 `/quiet` 參數所下載的 .EXE 檔案，以無訊息模式執行安裝。 例如：

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

如果您無法安裝 2016 可轉散發套件，請改為從這裡安裝 2010 可轉散發套件：[Microsoft Access Database Engine 2010 Redistributable](https://www.microsoft.com/download/details.aspx?id=13255) (Microsoft Access 資料庫引擎 2010 可轉散發套件)。 (沒有任何適用於 Excel 2013 的可轉散發套件。)

## <a name="specify-excel"></a> 開始使用

第一個步驟是指出您想要連接至 Excel。

### <a name="in-ssis"></a>在 SSIS 中
在 SSIS 中建立 Excel 連線管理員以連接至 Excel 來源或目的地檔案。 有數種方式可建立連線管理員：

-   在 [連線管理員] 區域，以滑鼠右鍵按一下然後選取 [新增連線]。 在 [新增 SSIS 連線管理員] 對話方塊中，依序選取 [EXCEL] 和 [新增]。
 
-   在 [SSIS] 功能表上，選取 [新增連線]。 在 [新增 SSIS 連線管理員] 對話方塊中，依序選取 [EXCEL] 和 [新增]。

-   當您在 [Excel 來源編輯器]或 [Excel 目的地編輯器] 的 [連線管理員] 頁面設定 [Excel 來源] 或 [Excel 目的地] 的同時建立連線管理員。

### <a name="in-the-sql-server-import-and-export-wizard"></a>在 [SQL Server 匯入和匯出精靈] 中
在 [匯入和匯出精靈] 的 [選擇資料來源] 或 [選擇目的地] 頁面上，選取 [資料來源] 清單中的 **Microsoft Excel**。

如果您在資料來源清單中看不到 Excel，請確定是否執行 32 位元精靈。 Excel 連線元件均通常是 32 位元檔案，在 64 位元精靈中不會顯示。

## <a name="excel-file"></a> Excel 檔案和檔案路徑

要提供資訊的第一項資訊是 Excel 檔案的路徑和檔案名稱。 提供此資訊的方式是使用 [Excel 連線管理員編輯器] 中的 SSIS 套件，或在 [匯入和匯出精靈] 的 [選擇資料來源] 或 [選擇目的地] 頁面。

以下列格式輸入路徑和檔案名稱：

-   本機電腦上的檔案為 **C:\\TestData.xlsx**。

-   網路共用上的檔案為 **\\\\Sales\\Data\\TestData.xlsx**。

或者，按一下 [瀏覽] 以使用 [開啟] 對話方塊找出試算表。  
  
> [!IMPORTANT]
> 您不能連接至受密碼保護的 Excel 檔案。

## <a name="excel-version"></a> Excel 版本

要提供的第二項資訊是 Excel 檔案的版本。 提供此資訊的方式是使用 [Excel 連線管理員編輯器] 中的 SSIS 套件，或在 [匯入和匯出精靈] 的 [選擇資料來源] 或 [選擇目的地] 頁面。

選取用於建立檔案的 Microsoft Excel 版本，或另一個相容版本。 例如，如果您無法安裝 2016 連線元件，您可以安裝 2010 元件並選取此清單中的 [Microsoft Excel 2007-2010]。

如果您只安裝了較舊版本的連線元件，可能無法選取清單中的較新 Excel 版本。 **Excel 版本**清單包含 SSIS 支援的所有 Excel 版本。 這份清單中的項目存在並不表示已安裝必要的連線元件。 例如，即使您尚未安裝 2016 連線元件，**Microsoft Excel 2016** 也會出現在清單中。

## <a name="first-row"></a> 第一個資料列具有資料行名稱

如果您從 Excel 匯入資料，下一個步驟就是指出資料的第一個資料列是否包含資料行名稱。 提供此資訊的方式是使用 [Excel 連線管理員編輯器] 中的 SSIS 套件，或在 [匯入和匯出精靈] 的 [選擇資料來源] 頁面上。

-   如果因為來源資料未包含資料行名稱而停用此選項，精靈會使用 F1、F2 等作為資料行標題。
-   如果資料包含資料行名稱，但您停用了此選項，則精靈會將資料行名稱匯入為資料的第一列。
-   如果資料不包含資料行名稱，但您啟用了此選項，則精靈會將來源資料的第一列用來作為資料行名稱。 在此情況下，來源資料的第一列已不再包含在資料本身。

如果您要從 Excel 匯出資料，且啟用了此選項，則匯出資料的第一列會包含資料行名稱。

## <a name="sheets-ranges"></a> 工作表和範圍

有三種 Excel 物件可以作為資料的來源或目的地：工作表、您指定位址的資料格具名範圍或未具名範圍。

-   **工作表。** 若要指定工作表，請在工作表名稱結尾加上 `$` 字元，並以分隔符號括住字串，例如 **[Sheet1$]**。 或者，在現有資料表和檢視的清單中，尋找結尾為 `$` 字元的名稱。

-   **命名範圍。** 若要指定命名範圍，請提供範圍名稱，例如 **MyDataRange**。 或者，在現有資料表和檢視的清單中，尋找結尾不是 `$` 字元的名稱。
    
-   **未命名範圍。** 若要指定尚未命名的儲存格範圍，請在工作表名稱結尾加上 $ 字元、指定範圍，再以分隔符號括住字串，例如 **[Sheet1$A1:B4]**。

若要選取或指定您想要用作資料來源或目的地的 Excel 物件類型，請執行下列事項之一：

### <a name="in-ssis"></a>在 SSIS 中

在 SSIS 中，在 [Excel 來源編輯器] 或 [Excel 目的地編輯器] 的 [連線管理員] 頁面上，執行下列事項之一：

-   若要使用**工作表**或**具名範圍**，請選取 [資料表或檢視] 作為 [資料存取模式]。 然後，在 [Excel 工作表的名稱] 清單中，選取工作表或具名範圍。

-   若要使用您指定位址的**未具名範圍**，請選取 [SQL 命令] 作為 [資料存取模式]。 然後，在 [SQL 命令文字] 欄位中，輸入類似下列範例的查詢：

    ```sql
    SELECT * FROM [Sheet1$A1:B5]
    ```

### <a name="in-the-sql-server-import-and-export-wizard"></a>在 [SQL Server 匯入和匯出精靈] 中
在 [匯入和匯出精靈] 中，執行下列其中一項：

-   當您從 Excel **匯入**時，執行下列其中一項：

    -   若要使用**工作表**或**具名範圍**，請在 [Specify table copy or query] (指定資料表複製或查詢) 畫面，選取 [Copy data from one or more tables or views] (從一或多個資料表或檢視複製資料)。 然後，在 [Select Source Tables and Views] 選取來源資料表和檢視) 頁面上，於 [來源] 資料行中，選取來源工作表及具名範圍。

    -   若要您使用指定位址的**未具名範圍**，請在 [Specify table copy or query] (指定資料表複製或查詢) 頁面上，選取 [Write a query to specify the data to transfer] (撰寫查詢來指定要傳送的資料)。 然後，在 [Provide a Source Query] (提供來源查詢) 頁面上，提供類似於下列範例的查詢：

        ```sql
        SELECT * FROM [Sheet1$A1:B5]
        ```

-   當您**匯出** Excel 時，執行下列其中一項：

    -   若要使用**工作表**或**具名範圍**，請在 [Select Source Tables and Views] (選取來源資料表和檢視) 頁面上的 [目的地] 資料行中，選取目的地工作表與具名範圍。

    -   若要使用指定位址的**未具名範圍**，請在 [Select Source Tables and Views] (選取來源資料表和檢視) 頁面的 [目的地] 資料行中，以不含分隔符號的下列格式輸入範圍：`Sheet1$A1:B5`。 精靈會新增分隔符號。

選取或輸入要匯入或匯出的 Excel 物件之後，您也可以在精靈的 [Select Source Tables and Views] (選取來源資料表和檢視) 頁面上執行下列動作：

-   選取 [編譯對應] 來檢閱來源與目的地之間的資料行對應。

-   預覽範例資料，選取 [預覽] 以確定它如您的預期。

## <a name="issues-types"></a> 資料類型的問題

### <a name="data-types"></a>資料類型

Excel 驅動程式只能辨識有限的一組資料類型。 例如，所有的數值資料行都會被解譯為倍整數 (DT_R8)，而所有的字串資料行 (備忘錄資料行除外) 全都會被解譯成 255 個字元的 Unicode 字串 (DT_WSTR)。 SSIS 對應 Excel 資料類型的情況如下：

-   數值 – 雙精確度浮點數 (DT_R8)

-   貨幣 – 貨幣 (DT_CY)

-   布林值 – 布林值 (DT_BOOL)

-   日期/時間 – datetime (DT_DATE)

-   字串 – Unicode 字串，長度 255 (DT_WSTR)

-   備忘錄 – Unicode 文字資料流 (DT_NTEXT)

### <a name="data-type-and-length-conversions"></a>資料類型和長度轉換

SSIS 不會隱含地轉換資料類型。 因此，您可能必須使用衍生的資料行轉換或資料轉換，在將 Excel 資料載入至非 Excel 目的地之前明確轉換 Excel 資料，或是在將資料載入至 Excel 目的地之前，轉換來自非 Excel 來源的資料。

以下是一些可能需要的轉換範例：  
  
-   Unicode Excel 字串資料行與具有特定字碼頁之非 Unicode 字串資料行之間的轉換。
  
-   255 個字元之 Excel 字串資料行與不同長度之字串資料行之間的轉換。
  
-   雙精確度 Excel 數值資料行與其他類型之數值資料行之間的轉換。

> [!TIP]
> 如果您使用 [匯入和匯出精靈]，且您的資料需要這其中的某些轉換，精靈會為您設定所需的轉換。 因此，即使是您想要使用 SSIS 套件時，使用 [匯入和匯出精靈] 來建立初始套件可能會很實用。 讓精靈為您建立並設定連線管理員、來源、轉換和目的地。

## <a name="issues-importing"></a> 匯入的問題

### <a name="empty-rows"></a>空的資料列

當您指定工作表或具名範圍為來源時，驅動程式會讀取「連續的」資料格區塊，從工作表或範圍左上角的第一個非空白資料格開始。 因此，您的資料不需要從資料列 1 開始，但您的來源資料中不能有空的資料列。 例如，您不能在資料行標題與資料列之間有空的資料列，或是標題後面接著在工作表頂端有空的資料列。

如果資料上方有空的資料列，便無法作為工作表來查詢資料。 在 Excel 中，您必須選取資料範圍並將名稱指派給該範圍，然後查詢具名範圍，而不是工作表。

### <a name="missing-values"></a>遺漏值

Excel 驅動程式會在指定來源中讀取特定資料列數目 (依預設為八個資料列)，以猜測各資料行的資料類型。 當資料行可能包含混合資料類型，尤其是數值資料與文字資料混合時，驅動程式會做出有利於大部分資料類型的決定，並於包含其他類型資料的資料格中傳回 Null 值。 (在繫結中，以數值類型優先)。Excel 工作表中大部分的資料格格式化選項，似乎都不會影響這項資料類型決定。

您可以藉由指定「匯入模式」將所有值當作文字匯入，來修改 Excel 驅動程式的這項行為。 若要指定「匯入模式」，請在 [屬性] 視窗中將 `IMEX=1` 新增到 Excel 連線管理員之連接字串中的 [擴充屬性] 值。 

### <a name="truncated-text"></a>截斷的文字

當驅動程式判斷出某個 Excel 資料行包含文字資料時，驅動程式將會根據其取樣的最長值來選取資料類型 (字串或備忘錄)。 如果驅動程式未在其取樣的資料列中發現任何長度超過 255 個字元的值，則會將該資料行視為 255 個字元字串資料行而非備忘錄資料行 因此，長度超過 255 個字元的值可能會被截斷。

若要從備忘資料行匯入資料而不截斷，您有兩個選項：

-   確定至少一個取樣的資料列中的備忘錄資料行，包含長度超過 255 個字元的值

-   增加驅動程式取樣的資料列數目，以包含這類資料列。 您可以提高下列登錄機碼下的 **TypeGuessRows** 值，藉以增加取樣的資料列數目：

| 可轉散發套件的元件版本 | 登錄機碼 |
|---|---|
| Excel 2016 | HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\16.0\Access Connectivity Engine\Engines\Excel |
| Excel 2010 | HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\14.0\Access Connectivity Engine\Engines\Excel |
| | |

## <a name="issues-exporting"></a> 匯出的問題

### <a name="create-a-new-destination-file"></a>建立新的目的地檔案

#### <a name="in-ssis"></a>在 SSIS 中

建立 Excel 連線管理員，並使用您想要建立的新 Excel 檔案路徑和檔案名稱。 然後，在 [Excel 目的地編輯器] 中，針對 [Excel 工作表名稱] 選取 [新增]建立目的地工作表。 此時，SSIS 會使用指定的工作表，建立新的 Excel 檔案。

#### <a name="in-the-sql-server-import-and-export-wizard"></a>在 [SQL Server 匯入和匯出精靈] 中

在 [選擇目的地] 頁面上，選取 [瀏覽]。 在 [開啟] 對話方塊方塊中，覽至您想要用來建立新 Excel 檔案的資料夾、提供新檔案的名稱，然後選取 [開啟]。

### <a name="export-to-a-large-enough-range"></a>匯出到夠大的範圍

當您將範圍指定為目的地時，如果範圍的「資料行」數目比來源資料還要少，則會發生錯誤。 不過，如果您所指定範圍的「資料列」數目比來源資料還要少，則精靈會繼續寫入資料列而不會有錯誤，並且會延伸範圍定義，以符合新的資料列數目。

### <a name="export-long-text-values"></a>匯出長文字值

在 Excel 資料行中成功儲存長於 255 個字元的字串之前，驅動程式必須能將目的地資料行的資料類型辨識為 **備忘** ，而不是 **字串**。

-   如果現有目的地資料表已包含資料列，則驅動程式所取樣的前幾個資料列必須在備忘資料行中至少包含一個值長於 255 個字元的執行個體。

-   如果在套件設計期間或在執行階段或由 [匯入和匯出精靈] 建立新的目的地資料表，則 `CREATE TABLE` 陳述式必須使用 LONGTEXT (或其同義字之一) 作為目的地備忘資料行的資料類型。 在精靈中，按一下 [資料行對應] 頁面的 [建立目的地資料表] 選項旁邊的 [編輯 SQL]，檢查 `CREATE TABLE` 陳述式並做必要的修訂。

## <a name="related-content"></a>相關內容

如需本文中所述的元件和程序的詳細資訊，請參閱下列文章：

### <a name="about-ssis"></a>關於 SSIS
[Excel 連線管理員](connection-manager/excel-connection-manager.md)  
[Excel 來源](data-flow/excel-source.md)  
[Excel 目的地](data-flow/excel-destination.md)  
[使用 Foreach 迴圈容器來執行 Excel 檔案和資料表迴圈](control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
[以指令碼工作處理 Excel 檔案](extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)

### <a name="about-the-sql-server-import-and-export-wizard"></a>關於 SQL Server 匯入和匯出精靈
[連接至 Excel 資料來源](import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)  
[透過匯入和匯出精靈的簡單範例開始使用](import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

### <a name="other-articles"></a>其他文章
[將 Excel 中的資料匯入 SQL Server 或 Azure SQL Database](../relational-databases/import-export/import-data-from-excel-to-sql.md)  
