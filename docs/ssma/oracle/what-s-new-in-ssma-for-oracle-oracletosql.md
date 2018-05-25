---
title: SSMA for Oracle (OracleToSQL) 中最新消息 |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-oracle
ms.custom: ''
ms.date: 03/01/2018
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
caps.latest.revision: 24
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d80bf7637c5c17cdade7c47f25265a6d2b6c94c1
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>SSMA for Oracle (OracleToSQL) 中最新消息
本主題列出每個版本中的 Oracle 變更 SSMA。  

## <a name="ssma-v77"></a>SSMA v7.7
SSMA for Oracle 的 v7.7 版本包含下列變更：
- SSMA for Oracle 已經增強，以改善品質和轉換的度量資訊的目標修正。
- 32 位元版本的 SSMA for Oracle 根據需要常用，已經恢復。 相較於之前的實作 （前 v7.4)，有兩個安裝程式套件，但是它們無法並存安裝。 如此一來，您必須選擇最適當版本根據連接元件。 一律最好是盡可能使用 64 位元版本。
- SQL Server 2017 現已支援官方 Oracle 延伸模組組件，也支援在 Linux 上 （新的遠端安裝選項）。 請注意，延伸模組組件功能限制在 Linux 上安裝時不支援的測試人員和伺服器端資料移轉功能 
- SSMA for Oracle 可讓您移轉具體化檢視表做為一般資料表 (可透過在設定**專案設定** -> **同步** ->  **具體化檢視探索備份資料表**)。

> [!IMPORTANT]
> SSMA v7.4 和更新版本，.Net 4.5.2 是安裝必要條件。

## <a name="ssma-v76"></a>SSMA v7.6
SSMA for Oracle 的 v7.6 版本已經過增強，改善品質和轉換的度量資訊的目標修正程式與 SQL Server 2017 （公開預覽狀態） 的支援。 支援在 Windows 和 Linux 上的 SQL Server 2017 是公開預覽狀態，而且不應該用於實際執行移轉。

> [!IMPORTANT]
> SSMA v7.4 和更新版本，.Net 4.5.2 為安裝必要元件，而 32 位元版本的工具已停用。

## <a name="ssma-v75"></a>SSMA v7.5
SSMA for Oracle 的 v7.5 版本包含下列變更：
- 增強，以確保行動不便人士更大的存取範圍的數個增強功能。
- 更新，可改善品質和轉換度量與目標的修正程式，例如改善處理日期和 float 資料類型的資料移轉期間，根據客戶的意見反應。

> [!IMPORTANT]
> .Net 4.5.2 是安裝 SSMA v7.5 的必要條件。 此外，開頭 v7.4，32 位元版本的 SSMA 會停止。

## <a name="ssma-v74"></a>SSMA v7.4
SSMA for Oracle 的 v7.4 版本包含下列變更：

- SSMA for Oracle 現在支援 Azure SQL 資料倉儲，做為目標平台進行移轉。

    ![新增專案 視窗](../media/new-project.png)
  - 支援的資料倉儲儲存體選項，如下列影像所示：

    ![資料倉儲儲存體選項](../media/storage-options_red.png)
  - 支援的資料分佈選項，如下列影像所示：

    ![資料倉儲的資料分佈](../media/data-distribution_red.png)

- **查詢逾時**選項現在時仍可使用在來源和目標結構描述物件探索。

    ![查詢逾時選項](../media/query-timeout_red.png)

- 品質和轉換的度量，而改善了目標的修正程式，根據客戶的意見反應。

> [!IMPORTANT]
> .Net 4.5.2 是安裝 SSMA v7.4 的必要條件。 此外，開頭 v7.4，32 位元版本的 SSMA 會停止。

## <a name="ssma-v73"></a>SSMA v7.3
SSMA for Oracle 的 v7.3 版本包含下列變更：
- 改善的品質和轉換的度量根據客戶的意見反應目標的修正程式。
- 透過下列項目公開 SSMA 擴充性架構：
  - 匯出至 SQL Server Data Tools (SSDT) 專案的功能。
    -   您現在可以在 SSDT 專案，從 SSMA 匯出結構描述指令碼。 您可以使用結構描述指令碼來進行額外的結構描述變更及部署您的資料庫。
![將儲存為 SSDT 專案命令](../media/export-schema-scripts_red.png)
  - 可供 SSMA 執行自訂轉換執行的程式庫。
    - 您現在可以建構自訂語法轉換和 SSMA 先前未處理的轉換可以處理的程式碼。
      - 這個部落格文章，指示如何建構自訂轉換子可用[擴充 SQL Server 移轉小幫手的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      - 下載範例專案，從這個轉換[部落格文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)。


## <a name="ssma-v72"></a>SSMA v7.2
SSMA for Oracle 的 v7.2 版本包含下列變更：
- 改善的品質和轉換的度量根據客戶的意見反應目標的修正程式。
- 遙測增強功能提供更好的資料點，來解決客戶問題，並改善 SSMA 的轉換比率。

## <a name="ssma-v71"></a>SSMA 7.1 版
7.1 版版本的 SSMA for Oracle 包含下列變更：
- 在 Windows 和 Linux CTP1 上的 SQL Server 2017 已移轉的支援的目標平台。 此功能是 technical preview 中，並可讓結構描述和資料移動到目標 SQL 伺服器。
- SSMA 現在支援自動更新，以下載最新版本的 SSMA，如有的話。
- SSMA 可安裝二進位檔現在都是透過 Windows installer 封裝檔案 (.msi) 提供。

**資源**

[擴充 SQL Server 移轉小幫手的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[評估並將資料從非 Microsoft 資料平台移轉到 SQL Server *（與 Oracle 範例）*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>2016 年  
2016 年版本的 SSMA for Oracle 包含下列變更：  

- 已新增的支援 SQL Server 2016。
- 加入至 SQL Server 的時態表 Oracle 回溯封存資料表的轉換。

    **請注意**-SSMA 不會複製從 Oracle 回溯資料封存資料表的歷程記錄資料。 如此一來，必須手動複製的歷程記錄資料移轉的程序。 此外，SSMA 不會在 SQL Server 中繼資料總管 顯示歷程記錄資料表，因為它會被視為系統資料表，而您可以在 SQL Server Management Studio 中檢視歷程記錄資料表。
    SQL Server 2016 中不支援數個 Oracle 回溯功能，包括：
    - Oracle 回溯交易查詢
    - DBMS_FLASHBACK 封裝
    - 回溯交易
    - 回溯資料封存
    - 回溯資料表
    - 回溯拖放
    - 回溯資料庫
- 加入的 SQL Server 原則物件 （Oracle 的資料列層級安全性） 的 Oracle VPD 原則轉換。
- Oracle 的初始載入時間降低。
- 改良的剖析和解析程式。
- 移除安裝程式檢查適用於.Net 2.0。
- 更新擴充功能組件相依性從.Net 3.5.net 4.0。
- 修正 儲存專案 」 以及 「 開啟專案 」 SSMA 主控台命令。
- SSMA 主控台的固定"securepassword"命令。
- 已修正的初始載入的物件計數。
- 修正 for Oracle 的字元資料類型轉換。
- 通用設定 中修正的 bug。
  
## <a name="march-2016"></a>2016 年 3 月  
2016 年 3 月預覽版本的 SSMA for Oracle 包含下列變更：  
  
-   移轉至 SQL Server 2016 所加入的支援。  
-   已新增的支援移轉 Oracle 的資料列層級安全性 （有限制）。  
-   針對移轉新增支援在記憶體中的 Oracle 資料表中，以 SQL Server 資料行存放區。  
  
## <a name="january-2016"></a>2016 年 1 月  
2014 年 1 月維護版的 SSMA for Oracle 包含下列變更：  
  
-   加入叢集索引的支援。  
-   修正過慢的 Oracle 結構描述查詢 (RFC 5076207)。  
-   固定從主控台連線至 Azure。  
-   加入的檢視要 SSMA (建議 RFC 5706203) 的記錄檔 功能表項目。 
-   加入的遙測。  
  
## <a name="july-2014"></a>2014 年 7 月  
2014 年 7 月版本的 SSMA for Oracle 包含下列變更：  
  
-   加入的 Azure SQL DB 支援。  
-   延伸模組組件的功能移至結構描述，以支援 Azure SQL DB。  
-   加入的 Oracle 具體化檢視的支援。  
-   已新增的支援 SQL Server 2014 記憶體最佳化的資料表。  
-   包含的效能改進測試包含超過 10k 之資料庫的物件。  
-   已加入的 UI 增強功能來處理大量的物件。  
-   加入的 「 已知 」 的 LOB 結構描述反白顯示。  
-   包括轉換速度的改良。  
-   UI 中的計數加入顯示物件的支援。  
-   減少的報表的大小超過 25%。
-   未剖析建構的改良的錯誤訊息。  
  
## <a name="april-2014"></a>2014 年 4 月  
2014 年 4 月發行的 SSMA for Oracle 包含下列變更：  
  
-   已新增的支援 MS SQL Server 2014。  
-   已新增的支援 Oracle 12 和查詢的最佳化。  
-   關於 Azure 的轉換已經修正的 bug。  
-   關於不可見的報表頁面在 IE 10 中已修正的 bug。  
  
## <a name="january-2012"></a>2012 年 1 月  
2012 年 1 月版本的 SSMA for Oracle 包含下列變更：  
  
-   加入資料列型別和 RecordType 輸入參數的支援預設為 NULL。  
  
## <a name="july-2011"></a>2011 年 7 月  
2011 年 7 月版本的 SSMA for Oracle 包含下列變更：  
  
-   加入支援的 Oracle 順序轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"順序產生器。  
-   在資料遷移期間報告改良的錯誤。  
-   改進的轉換的陳述式使用保留的字。  
-   改善的函式中的日期值的隱含轉換。  
  
## <a name="april-2011"></a>2011 年 4 月  
2011 年 4 月發行的 SSMA for Oracle 包含下列變更：  
  
-   彙總支援的"SSMA for Oracle"產品[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005 年[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2008年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"。  
-   加入連接及移轉至支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"。  
-   增強型的用戶端資料移轉引擎，支援平行的資料移轉。  
-   提升的資料移轉效能簡單與大量記錄復原模式。  
-   已新增的支援回溯相容性的先前版本的 SSMA （v4.0 和 4.2 版） 所建立的專案。  
-   加入 Oracle v5.0 產品的並存 (SxS) 與舊版本的 SSMA （v4.0 和 4.2 版） 安裝 SSMA 的能力。  
-   已新增的支援報告 （包括子類型、 VARRAY、 巢狀資料表、 物件資料表和物件檢視） 的使用者定義類型和其使用方式的 PL/SQL 區塊使用特殊的錯誤訊息。  

## <a name="july-2010"></a>2010 年 7 月  
SSMA for Oracle 的 2010 年 7 月發行版本包含下列變更：  
  
-   已新增的支援移轉至 SQL Server 2008 R2。  
-   加入新的 SSMA 主控台應用程式的命令列執行。  
-   已加入的伺服器端和用戶端資料移轉引擎所使用的資料移轉的支援。  
-   新增 「 自訂選取 」 中的資料移轉的陳述式的支援。  
-   已新增的支援從 Oracle 11g R2 進行移轉。  
  
## <a name="june-2008"></a>2008 年 6 月  
2008 年 6 月版本的 SSMA for Oracle 包含下列變更：  
  
-   評估報表中，包含同義字的其他資訊、 剖析物件、 面板和 SQL Server 標誌移除，和配置保存的未經處理資料來源已加入的增強功能。  
-   已加入的物件轉換中的增強功能：  
    -   套件 DBMS_LOB、 加入 DBMS_SQL 轉換。  
    -   聯結修訂的轉換。  
    -   集合和記錄轉換，現在在簡單案例中透過不同的變數，每個欄位發行記錄轉換的修改。  
    -   改進的記錄和集合的實作。  
    -   視窗型彙總函式加入。  
    -   新增彙總套件/CUBE 子句。  
    -   NEXTVAL/CURVAL 的改進。  
    -   在 SET 子句中群組資料行，已加入群組集合，與群組識別碼。  
    -   MERGE 陳述式加入。  
    -   新的日期時間類型和 CLR 資料型別加入記錄和集合轉換支援。  
-   加入新的功能，測試人員。 資料表現在可以測試以使用 Tester 物件、 測試案例中的數個可測試物件的呼叫順序可以改變、 使用者可以測試程序和函式與記錄和做為參數的集合，並將傳回值，而加入分析器檢查相依性只使用資料表。  
  
## <a name="august-2007"></a>2007 年 8 月  
2007 年 8 月版本的 SSMA for Oracle 包含下列變更：  
  
-   加入新的測試人員元件可讓您建立、 管理及執行測試案例，以確認已轉換的 SQL 程式碼。  
-   已加入轉換的 Oracle 子型別、 集合和本機模組已新增的支援 SQL 轉換器。  
-   加入新的同步處理功能可讓您同步處理與 SQL Server 資料庫的特定物件。  
-   加入新的轉換選項。  
  
## <a name="april-2007"></a>2007 年 4 月  
2007 年 4 月版的 SSMA for Oracle 是最早的版本。
