---
title: 什麼是 SSMA for Oracle (OracleToSQL) 新功能 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 09/22/2018
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: bc54f3046ec3163e3d480dd6feae906368fa4c12
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52405995"
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>SSMA for Oracle (OracleToSQL) 中最新消息
本文章列出 SSMA 中每個版本的 Oracle 變更。  

## <a name="ssma-v710"></a>SSMA v7.10
SSMA for Oracle 的 v7.10 版本包含下列變更：
- 目標式的修正，旨在提供額外的安全性和隱私權保護，以符合全球需求的變更。
- 轉換改善，與階層式查詢。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件。

## <a name="ssma-v79"></a>SSMA v7.9
SSMA for Oracle 的 v7.9 版本包含下列變更：
- 目標式的修正，可改善品質和轉換的計量。
- 移轉 [繼續] 陳述式支援從 Oracle 到 SQL Server。
- 支援變更資料類型對應和專案的喜好設定的 SSMA 命令列中。
- 支援移轉使用 SQL Server Integration Services (SSIS) 資料。 轉換結構描述之後, 就可以建立 SSIS 封裝，透過右鍵操作功能表選項。
- SSMA 中的 [Azure SQL Database 連接] 對話方塊也已經改變指定完整的伺服器名稱。 在舊版的 SSMA，Azure SQL Database 的前置詞必須明確提及在專案設定。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件。

## <a name="ssma-v78"></a>SSMA v7.8
SSMA for Oracle 的 v7.8 版本包含下列變更：
-   已新增的支援：
    - IN 子句的資料列運算式。
    - 隱含類型轉換 （cast)。
    - Azure SQL Database 的 UID 轉換。
- 專案設定中的反白顯示的變更型別對應。
- 提供可讓使用者以停用遙測。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件。

## <a name="ssma-v77"></a>SSMA v7.7
SSMA for Oracle 的 v7.7 版本包含下列變更：
- SSMA for Oracle 已改良，提供目標式修正，可改善品質和轉換的計量。
- 32 位元版本的 SSMA for Oracle 依據熱門的需求，已經恢復。 相較於先前的實作 （在之前 v7.4)，有兩個安裝程式套件，但它們無法並存安裝。 如此一來，您必須選擇您所擁有的最適當版本的連線元件為基礎。 一律最好是使用 64 位元版本，如果可能的話。
- SQL Server 2017 現已支援官方 Oracle 延伸模組組件也支援在 Linux 上 （新的遠端安裝選項）。 請注意，延伸模組組件功能有限時安裝在 Linux 上，為測試人員並不支援伺服器端資料移轉功能。
- SSMA for Oracle 可讓您移轉具體化檢視表做為一般資料表 (可透過設定的設定**專案設定** -> **同步處理** ->  **具體化檢視探索支援資料表**)。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件。

## <a name="ssma-v76"></a>SSMA v7.6
SSMA for Oracle 的 v7.6 版本已經過加強，改善品質和轉換計量的目標式修正與 SQL Server 2017 （公開預覽） 的支援。 在 Windows 和 Linux 上的 SQL Server 2017 支援處於公開預覽狀態，並不應該用於實際執行移轉。

> [!IMPORTANT]
> SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件，與 32 位元版本的工具已停用。

## <a name="ssma-v75"></a>SSMA v7.5
SSMA for Oracle 的 v7.5 版本包含下列變更：
- 增強的幾項改進，以確保更高的協助工具，方便殘障人士使用。
- 更新，以提升的品質和轉換的計量，與目標式修正，例如處理日期和 float 資料類型的資料在移轉期間，根據客戶意見反應。

> [!IMPORTANT]
> .Net 4.5.2 是安裝 SSMA v7.5 的必要條件。 此外，開頭為 v7.4，32 位元版本的 SSMA 即將中止。

## <a name="ssma-v74"></a>SSMA v7.4
SSMA for Oracle 的 v7.4 版本包含下列變更：

- SSMA for Oracle 現在支援 Azure SQL 資料倉儲，做為移轉的目標平台。

    ![新增專案 視窗](../media/new-project.png)
  - 支援資料倉儲儲存體選項，如下圖所示：

    ![資料倉儲的儲存體選項](../media/storage-options_red.png)
  - 支援資料分佈選項，如下圖所示：

    ![資料倉儲的資料分佈](../media/data-distribution_red.png)

- **查詢逾時**選項已經可以使用在來源和目標結構描述物件探索期間。

    ![查詢逾時選項](../media/query-timeout_red.png)

- 品質和轉換的計量，而改善了目標式修正，根據客戶意見反應。

> [!IMPORTANT]
> .Net 4.5.2 是安裝 SSMA v7.4 的必要條件。 此外，開頭為 v7.4，32 位元版本的 SSMA 即將中止。

## <a name="ssma-v73"></a>SSMA v7.3
SSMA for Oracle 的 v7.3 版本包含下列變更：
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
SSMA for Oracle 的 v7.2 版本包含下列變更：
- 改善的品質和轉換度量目標式修正，根據客戶意見反應。
- 若要提供更好的資料點，來解決客戶問題，並改善 SSMA 的轉換率的遙測增強功能。

## <a name="ssma-v71"></a>SSMA 7.1 版
7.1 版版本的 SSMA for Oracle 包含下列變更：
- 在 Windows 和 Linux CTP1 上的 SQL Server 2017 現支援的目標平台進行移轉。 這項功能是在 technical preview 中，並允許結構描述和資料移動至目標 SQL server。
- SSMA 現在支援自動更新，以下載最新版本的 SSMA，因為它位於。
- SSMA 安裝二進位檔現在都是透過 Windows installer 套件檔案 (.msi) 提供。

**資源**

[擴充 SQL Server Migration Assistant 的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[評估並將資料從非 Microsoft 資料平台移轉至 SQL Server *（含 Oracle 範例）*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>2016 年  
2016 年版本的 SSMA for Oracle 包含下列變更：  

- 已新增的支援 SQL Server 2016。
- 已新增至 SQL Server 的時態表 Oracle 倒敘封存資料表的轉換。

    **請注意**-SSMA 不複製 Oracle 倒敘資料封存資料表的歷程記錄資料。 如此一來，必須手動複製歷程記錄資料移轉的程序。 此外，雖然 SSMA 不在 SQL Server 中繼資料總管 中顯示歷程記錄資料表，因為它會被視為系統資料表，您就可以在 SQL Server Management Studio 中檢視歷程記錄資料表。
    SQL Server 2016 不支援數個 Oracle 倒敘功能，包括：
    - Oracle 倒敘交易查詢
    - DBMS_FLASHBACK 封裝
    - 倒敘交易
    - 倒敘資料封存
    - 倒敘資料表
    - 倒敘拖放
    - 快閃回復資料庫
- 已新增至 SQL Server 原則物件 （適用於 Oracle 的資料列層級安全性） 的 Oracle VPD 原則轉換。
- 適用於 Oracle 的初始載入時間減少。
- 改進的剖析和解析程式。
- 已移除適用於.Net 2.0 的安裝程式檢查。
- 更新延伸模組組件相依性從.Net 3.5 到.Net 4.0。
- 已修正 儲存專案 」 和 SSMA 主控台的 開啟專案 命令。
- SSMA 主控台中修正 「 securepassword"命令。
- 已修正的初始載入的物件計數。
- 已修正適用於 Oracle 的字元資料類型轉換。
- 全域設定中已修正的 bug。
  
## <a name="march-2016"></a>2016 年 3 月  
SSMA for Oracle 的 2016 年 3 月預覽版本包含下列變更：  
  
-   新增的移轉至 SQL Server 2016 的支援。  
-   已新增的支援移轉 Oracle 的資料列層級安全性 （有一些限制）。  
-   新增移轉的支援在記憶體中的 Oracle 資料表中，以 SQL Server 資料行存放區。  
  
## <a name="january-2016"></a>2016 年 1 月  
2014 年 1 月的 SSMA for Oracle 的維護版本包含下列變更：  
  
-   已新增的支援叢集索引。  
-   已修正緩慢的 Oracle 結構描述查詢 (RFC 5076207)。  
-   已修正從主控台連線至 Azure。  
-   新增的檢視至 SSMA (RFC 5706203) 的記錄功能表項目。 
-   已新增的遙測。  
  
## <a name="july-2014"></a>2014 年 7 月  
SSMA for Oracle 的 2014 年 7 月版本包含下列變更：  
  
-   已新增適用於 Azure SQL DB 的支援。  
-   延伸模組組件功能移至結構描述以支援 Azure SQL DB。  
-   已新增的支援 Oracle 具體化的檢視。  
-   已新增的支援 SQL Server 2014 記憶體最佳化的資料表。  
-   包含的效能改進測試針對具有超過 10 萬元的資料庫物件。  
-   已新增的 UI 增強功能來處理大量的物件。  
-   新增的 「 已知 」 的 LOB 結構描述反白顯示。  
-   包含轉換速度改善。  
-   已新增的支援，來顯示物件計數的 UI 中。  
-   減少的報表的大小超過 25%。
-   未剖析的建構的改良的錯誤訊息。  
  
## <a name="april-2014"></a>2014 年 4 月  
SSMA for Oracle 的 2014 年 4 月版本包含下列變更：  
  
-   已新增的 MS SQL Server 2014 的支援。  
-   已新增的支援 Oracle 12 和查詢的最佳化。  
-   關於轉換至 Azure 已經修正的 bug。  
-   已修正的 IE 10 中的不可見的報表頁面相關的 bug。  
  
## <a name="january-2012"></a>2012 年 1 月  
SSMA for Oracle 的 2012 年 1 月版本包含下列變更：  
  
-   已新增的支援的資料列型別和 RecordType 輸入參數預設為 NULL。  
  
## <a name="july-2011"></a>2011 年 7 月  
SSMA for Oracle 的 2011 年 7 月版本包含下列變更：  
  
-   新增支援的 Oracle 順序，以轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"Denali"序列產生器。  
-   資料移轉期間報告改良的錯誤。  
-   使用保留的字的陳述式的改善的轉換。  
-   改善函式中的日期值的隱含轉換。  
  
## <a name="april-2011"></a>2011 年 4 月  
SSMA for Oracle 的 2011 年 4 月版本包含下列變更：  
  
-   彙總支援的"SSMA for Oracle"產品[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005年[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"Denali"。  
-   已新增支援連接，並移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"Denali"。  
-   增強型的用戶端資料移轉引擎，支援平行移轉資料。  
-   改善的資料移轉效能與簡單和大量記錄復原模式。  
-   已新增的支援回溯相容性的較早版本的 SSMA （v4.0 和 4.2 版） 所建立的專案。  
-   新增安裝 SSMA for Oracle v5.0 產品並存 (SxS) 與較舊版本的 SSMA （v4.0 和 4.2 版） 的能力。  
-   已加入的支援報告 （包括子型別、 VARRAY、 巢狀資料表、 物件資料表和物件檢視） 的使用者定義類型和其使用方式的 PL/SQL 區塊使用特殊的錯誤訊息。  

## <a name="july-2010"></a>2010 年 7 月  
SSMA for Oracle 的 2010 年 7 月版本包含下列變更：  
  
-   已新增的支援移轉至 SQL Server 2008 R2。  
-   加入新的 SSMA 主控台應用程式的命令列執行。  
-   已新增的支援使用伺服器端和用戶端資料移轉引擎的資料移轉。  
-   已新增的支援在資料移轉的 「 自訂選取 」 陳述式。  
-   已新增的支援從 Oracle 11g R2 移轉。  
  
## <a name="june-2008"></a>2008 年 6 月  
SSMA for Oracle 的 2008 年 6 月版本包含下列變更：  
  
-   新增的評定報告，包含同義字的其他資訊、 可剖析的物件、 面板和 SQL Server 標誌移除與配置保存的原始來源的功能改進。  
-   加入的物件轉換中的改進：  
    -   封裝 DBMS_LOB、 DBMS_SQL 轉換加入。  
    -   聯結修訂的轉換。  
    -   修改集合和記錄轉換，現在轉換釋出透過不同的變數，每個欄位的簡單案例中的記錄。  
    -   改進的記錄和集合的實作。  
    -   加入視窗型彙總函式。  
    -   加入 ROLLUP/CUBE 子句。  
    -   NEXTVAL/CURVAL 的改進。  
    -   在 SET 子句中群組資料行，已新增群組集合，與群組識別碼。  
    -   MERGE 陳述式加入。  
    -   新的日期時間類型和轉換成 CLR 資料類型加入記錄和集合的支援。  
-   已新增的軟體測試人員的新功能。 資料表現在可以測試做為物件使用軟體測試人員、 測試案例中的數個可測試物件的呼叫順序，可以改變、 使用者可以做為參數和傳回值，測試程序和函式記錄與集合和相依性解析程式新增至檢查只使用過的資料表。  
  
## <a name="august-2007"></a>2007 年 8 月  
SSMA for Oracle 的 2007 年 8 月版本包含下列變更：  
  
-   加入新的軟體測試人員元件可讓您建立、 管理及執行測試案例，若要確認轉換的 SQL 程式碼。  
-   已新增的支援的 Oracle 子型別、 集合和本機模組轉換已加入至 SQL 轉換子。  
-   加入新的同步處理功能可讓您與 SQL Server 資料庫同步處理特定的物件。  
-   加入新的轉換選項。  
  
## <a name="april-2007"></a>2007 年 4 月  
2007 年 4 月版本的 SSMA for Oracle 是初始版本。
