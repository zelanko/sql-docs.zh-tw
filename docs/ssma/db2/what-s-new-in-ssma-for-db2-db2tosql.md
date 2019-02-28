---
title: SSMA for DB2 中最新消息 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 02/27/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0254f57e5c653c68762159c7e51e71e70fa5fcd2
ms.sourcegitcommit: 2ab79765e51913f1df6410f0cd56bf2a13221f37
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/27/2019
ms.locfileid: "56955889"
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>SSMA for DB2 中最新消息 (DB2ToSQL)
本文章列出 SQL Server Migration Assistant (SSMA) 的每個版本中的 DB2 變更。

## <a name="ssma-v80"></a>SSMA v8.0
8.0 版版的 SSMA for DB2 已經過增強，以提供目標式的修正，旨在改善品質和轉換的計量。 此版本也提供了下列新功能：

* 支援**Azure SQL Database 受控執行個體**做為目標。 您現在可以建立新的專案目標 Azure SQL Database 受控執行個體：

    ![SQL DB MI 專案](../media/ssma-newproject-sqldbmi.png)

*   轉換後**修正 advisor**。 深入了解[此處](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)。

*   初步的資料庫/結構描述選取範圍。

    連接到來源時，使用者現在可以選取感興趣的資料庫/結構描述。 選取您要移轉的結構描述，會將儲存初始連線期間的時間，並改善整體的 SSMA 效能。

    ![SSMA 篩選物件](../media/ssma-filter-objects.png)

> [!IMPORTANT]
> 使用 SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件。

## <a name="ssma-v710"></a>SSMA v7.10
SSMA for DB2 的 v7.10 版本包含下列變更：
- 目標式的修正，旨在提供額外的安全性和隱私權保護，以符合全球需求的變更。
- 轉換 BEGIN END 區塊的修正。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件。

## <a name="ssma-v79"></a>SSMA v7.9
SSMA for DB2 的 v7.9 版本包含下列變更：
- 目標式的修正，可改善品質和轉換的計量。
- 支援變更資料類型對應和專案的喜好設定的 SSMA 命令列中。
- 支援移轉使用 SQL Server Integration Services (SSIS) 資料。 轉換結構描述之後, 就可以建立 SSIS 封裝，透過右鍵操作功能表選項。
- SSMA 中的 [Azure SQL Database 連接] 對話方塊也已經改變指定完整的伺服器名稱。 在舊版的 SSMA，Azure SQL Database 的前置詞必須明確提及在專案設定。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件。

## <a name="ssma-v78"></a>SSMA v7.8
SSMA for DB2 的 v7.8 版本包含下列變更：
- 專案設定中的反白顯示的變更型別對應。
- 提供可讓使用者以停用遙測。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件。

## <a name="ssma-v77"></a>SSMA v7.7
SSMA for DB2 的 v7.7 版本包含下列變更：
- SSMA for DB2 的增強提供目標式修正，可改善品質和轉換的計量。
- 32 位元版本的 SSMA for DB2 依據熱門的需求，已經恢復。 相較於先前的實作 （在之前 v7.4)，有兩個安裝程式套件，但它們無法並存安裝。 如此一來，您必須選擇您所擁有的最適當版本的連線元件為基礎。 一律最好是使用 64 位元版本，如果可能的話。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件。

## <a name="ssma-v76"></a>SSMA v7.6
已增強 v7.6 版的 SSMA for DB2，改善品質和轉換計量的目標式修正與 SQL Server 2017 （公開預覽） 的支援。 在 Windows 和 Linux 上的 SQL Server 2017 支援處於公開預覽狀態，並不應該用於實際執行移轉。

> [!IMPORTANT]
> SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件，與 32 位元版本的工具已停用。

## <a name="ssma-v75"></a>SSMA v7.5
增強 v7.5 版的 SSMA for DB2 提供幾項改進，以確保更高的協助工具，方便殘障人士使用。

> [!IMPORTANT]
> .Net 4.5.2 是安裝 SSMA v7.5 的必要條件。 此外，開頭為 v7.4，32 位元版本的 SSMA 即將中止。

## <a name="ssma-v74"></a>SSMA v7.4
SSMA for DB2 的 v7.4 版本包含下列變更：
- **查詢逾時**選項已經可以使用在來源和目標結構描述物件探索期間。
![查詢逾時選項](../media/query-timeout_red.png)

- 品質和轉換的計量，而改善了目標式修正，根據客戶意見反應。

> [!IMPORTANT]
> .Net 4.5.2 是安裝 SSMA v7.4 的必要條件。 此外，開頭為 v7.4，32 位元版本的 SSMA 即將中止。

## <a name="ssma-v73"></a>SSMA v7.3
SSMA for DB2 的 v7.3 版本包含下列變更：
- 改善的品質和轉換度量目標式修正，根據客戶意見反應。
- SSMA 擴充性架構，透過下列項目公開：
  - 匯出至 SQL Server Data Tools (SSDT) 專案的功能。
    -   您現在可以從 SSMA 匯出結構描述指令碼，SSDT 專案。 您可以使用結構描述指令碼來進行其他的結構描述變更及部署您的資料庫。
![將儲存為 SSDT 專案命令](../media/export-schema-scripts_red.png)
  - 可供執行自訂轉換的 SSMA 的程式庫。
    - 您現在可以建構自訂的語法轉換和轉換先前未處理的 SSMA 可以處理的程式碼。
      - 在此部落格文章中，可指示如何建構自訂轉換器[擴充 SQL Server Migration Assistant 的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      - 下載範例專案進行轉換，從此[部落格文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)。

## <a name="ssma-v72"></a>SSMA v7.2
SSMA for DB2 的 v7.2 版本包含下列變更：
- 改善的品質和轉換度量目標式修正，根據客戶意見反應。
- 若要提供更好的資料點，來解決客戶問題，並改善 SSMA 的轉換率的遙測增強功能。

## <a name="ssma-v71"></a>SSMA v7.1
SSMA for Access v7.1 版本包含下列變更：
- 在 Windows 和 Linux CTP1 上的 SQL Server 2017 現支援的目標平台進行移轉。 這項功能是在 technical preview 中，並允許結構描述和資料移動至目標 SQL server。
- SSMA 現在支援自動更新，以下載最新版本的 SSMA，因為它位於。
- SSMA 安裝二進位檔現在都是透過 Windows installer 套件檔案 (.msi) 提供。

**資源**

[擴充 SQL Server Migration Assistant 的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[評估並將資料從非 Microsoft 資料平台移轉至 SQL Server *（含 Oracle 範例）*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>2016 年  
2016 年版的 SSMA for DB2 會包含下列變更：  

-  已新增的支援 SQL Server 2016。
-  已新增到 SQL Server 記憶體中和 hekaton 功能 DB2 中的記憶體和一般資料表的轉換。
-  新增的轉換 DB2 存取控制為 SQL Server 原則物件 （for DB2 的資料列層級安全性）。
-  已新增至 SQL Server 的時態表的 DB2 系統建立版本資料表的轉換。
-  改善的 DB2 剖析和解析程式。
-  已移除適用於.Net 2.0 的安裝程式檢查。
-  從 Db2 安裝程式中移除不必要的 *.dll。
-  已修正 儲存專案 」 和 SSMA 主控台的 開啟專案 命令。
-  SSMA 主控台中修正 「 securepassword"命令。
-  已修正的初始載入的物件計數。
-  全域設定中已修正的 bug。
  
## <a name="march-2016"></a>2016 年 3 月  
2016 年 3 月預覽版本的 SSMA for DB2 會包含下列變更：  
  
-  新增的移轉至 SQL Server 2016 的支援。  
  
## <a name="january-2016"></a>2016 年 1 月  
2016 年 1 月維護版的 SSMA for DB2 會包含下列變更：  
  
-  已新增的支援的標準函式數目。  
-  已修正 DB2 剖析器錯誤。  
-  固定的 DB2 v9 zOS 支援 (RFC 5690920)。  
-  在轉換期間固定的 DB2 無法解析的識別項的錯誤。  
-  新增的檢視至 SSMA (RFC 5706203) 的記錄功能表項目。  
-  已新增的遙測。
  
## <a name="november-2014"></a>2014 年 11 月  
2014 年 11 月版的 SSMA for DB2 是初始版本。
