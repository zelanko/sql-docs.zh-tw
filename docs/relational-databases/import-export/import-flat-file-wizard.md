---
title: 將一般檔案匯入 SQL | Microsoft Docs
description: '[匯入一般檔案精靈] 是一個簡單的方法，可將 .csv、.txt 檔案的資料複製到新資料庫資料表。 本文說明如何及何時使用此精靈。'
ms.custom: ''
ms.date: 09/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: data-movement
ms.topic: conceptual
f1_keywords:
- sql13.swb.importflatfile.f1
author: yualan
ms.author: alayu
ms.reviewer: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 074dc46c36f4b90bebc241840eb137549e3bbd4d
ms.sourcegitcommit: 2b4baae583a5430f2e2ec76192ef1af3f55b25e8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/15/2020
ms.locfileid: "88251439"
---
# <a name="import-flat-file-to-sql-wizard"></a>將一般檔案匯入 SQL 精靈
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
> 如需 [匯入及匯出精靈] 的相關內容，請參閱 [SQL Server 匯入及匯出精靈](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard)。

[匯入一般檔案精靈] 是一個簡單的方法，可將一般檔案 (.csv、.txt) 的資料複製到您資料庫中的新資料表。 本概觀將說明使用此精靈的理由、如何找到此精靈，並提供簡單的範例供您參考。

## <a name="why-would-i-use-this-wizard"></a>為什麼要使用此精靈？
建立此精靈的目的在於改善目前的匯入體驗，運用稱之為 Program Synthesis using Examples ([PROSE](https://microsoft.github.io/prose/)) 的智慧型架構。 對於缺乏專業網域知識的使用者來說，匯入資料往往是件複雜、容易出錯且沉悶的工作。 此精靈簡化了匯入程序，只要選取輸入檔與唯一的資料表名稱，PROSE 架構就會為您處理其餘的部分。

PROSE 會分析輸入檔中的資料模式，來推斷資料行名稱、類型及分隔符號等項目。 此架構能夠理解檔案的結構，並會處理一切繁雜的作業程序，讓使用者省下大筆心力。

若要進一步了解 [匯入一般檔案] 精靈的使用者體驗改進，請觀賞這個影片：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-new-Import-Flat-File-Wizard-in-SSMS-173/player?WT.mc_id=dataexposed-c9-niner]

## <a name="prerequisites"></a>Prerequisites
只有 SQL Server Management Studio (SSMS) v17.3 或更新版本才提供此功能。 請確認目前使用的是最新版本。 您可以於[此處](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)找到最新版本。
 
## <a name="getting-started"></a><a id="started"></a>使用者入門
若要存取 [匯入一般檔案精靈]，請遵循這些步驟進行：

1. 開啟 [SQL Server Management Studio]  。
2. 連線至 SQL Server 資料庫引擎或 localhost 的執行個體。
3. 展開 [資料庫]  ，在資料庫上按一下滑鼠右鍵 (下方範例中的測試)，指向 [工作]  ，然後按一下 [匯入資料] 上方的 [匯入一般檔案]  。

![精靈功能表](media/import-flat-file-wizard/import-flat-file-menu.png)

若要深入了解精靈的不同功能，請參照下列教學課程：

## <a name="tutorial"></a>教學課程
在本課程中，您可隨意使用自己的一般檔案。 否則，本教學課程會使用下方來自 Excel 的 CSV，您也可任意複製。 如果您使用此 CSV，請將其標題命名為 **example.csv**，並記得將其儲存為 CSV，並置於方便的位置 (例如桌面)。

![精靈 Excel](media/import-flat-file-wizard/import-flat-file-example.png)

### <a name="step-1-access-wizard-and-intro-page"></a>步驟 1:存取精靈及簡介頁面
遵循[此處](#started)的說明存取精靈。

精靈的第一頁是歡迎頁面。 若不想再看到此頁面，可按一下 [不要再顯示此開始頁面]  。

![精靈簡介](media/import-flat-file-wizard/import-flat-file-intro.png)

### <a name="step-2-specify-input-file"></a>步驟 2:指定輸入檔
按一下 [瀏覽] 以選取輸入檔。 依預設，該精靈會搜尋 .csv 與 .txt 檔案。 

新的資料表名稱應為唯一，若名稱重複，精靈不會允許您前往下一步。

![精靈指定](media/import-flat-file-wizard/import-flat-file-specify.png)

### <a name="step-3-preview-data"></a>步驟 3：預覽資料
精靈會產生預覽，讓您檢視前 50 個資料列。 若有任何問題，請按一下 [取消]，否則請進入下一頁。

![精靈預覽](media/import-flat-file-wizard/import-flat-file-preview.png)

### <a name="step-4-modify-columns"></a>步驟 4：修改資料行
該精靈會找出其認為正確的資料行名稱、資料類型等等。若這些欄位不正確 (例如，資料類型應為 float，而非 int)，可於此處編輯。

準備完成後請繼續進行。

![精靈修改](media/import-flat-file-wizard/import-flat-file-modify.png)

### <a name="step-5-summary"></a>步驟 5：摘要
這只是顯示目前設定的摘要頁面。 若有問題，可返回先前的區段。 否則，請按一下 [完成] 以嘗試匯入程序。

![精靈摘要](media/import-flat-file-wizard/import-flat-file-summary.png)

### <a name="step-6-results"></a>步驟 6：結果
此頁面會指出匯入是否成功。 若出現綠色核取記號就表示成功，否則可能需要檢閱設定或輸出檔，以了解錯誤。

![精靈結果](media/import-flat-file-wizard/import-flat-file-results.png)

## <a name="troubleshooting"></a>疑難排解
匯入一般檔案精靈會根據前 200 個資料列來偵測資料類型。  在一般檔案中進一步的資料不符合自動偵測到之資料類型的情況下，將會在匯入期間發生錯誤。 錯誤訊息如下所示：
```
Error inserting data into table. (Microsoft.SqlServer.Prose.Import)
The given value of type String from the data source cannot be converted to type nvarchar of the specified target column. (System.Data)
String or binary data would be truncated. (System.Data)
```
減輕此錯誤的策略：
- 在[修改資料行步驟](#step-4-modify-columns)中擴充資料類型大小 (例如 Nvarchar 資料行的長度)，可能會補償一般檔案其餘部分之資料中的變化。
- 在[修改資料行步驟](#step-4-modify-columns)中啟用錯誤報告 (特別是較小的數字)，將顯示一般檔案中的哪些資料列包含不符合所選資料類型的資料。 例如，在第二個資料列引進錯誤的一般檔案中，執行匯入並產生範圍為 1 的錯誤報告，可提供特定的錯誤訊息。  直接在位置上檢查檔案，可根據已識別資料列中的資料，為資料類型提供更具目標的變更。

![錯誤報告結果](media/import-flat-file-wizard/import-flat-file-error.png)

```
Error inserting data into table occured while inserting rows 1 - 2. (Microsoft.SqlServer.Prose.Import)
The given value of type String from the data source cannot be converted to type float of the specified target column. (System.Data)
Failed to convert parameter value from a String to a Double. (System.Data)
```


## <a name="learn-more"></a>深入了解

深入了解精靈。
 
- **深入了解匯入其他來源。** 若想要匯入一般檔案之外的項目，請參閱 [ SQL Server 匯入及匯出精靈](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard)。
- **深入了解連線至一般檔案來源。** 若想要尋找連線至一般檔案來源的詳細資訊，請參閱[連線至一般檔案資料來源](https://docs.microsoft.com/sql/integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard)。
- **深入了解 PROSE。** 若想尋找此精靈使用之智慧型架構的概觀，請參閱 [PROSE SDK](https://microsoft.github.io/prose/)。

