---
title: SSMA for MySQL (MySQLToSql) 中最新消息 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 06/11/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
author: HJToland3
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 5f3ea9905f0a44e7863154b93283ea8ef2f49f7b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66841064"
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>SSMA for MySQL 的新功能 (MySqlToSql)

本文章列出 SQL Server Migration Assistant (SSMA) 的每個版本中的 MySQL 變更。

## <a name="ssma-v82"></a>SSMA v8.2

V8.1 版的 SSMA for MySQL 以一組目標的設計可以改善品質和轉換度量，以及修正的修正程式增強了：

* 資料移轉之後的已停用非叢集索引發生問題。
* 偵測.NET Framework 的無訊息安裝時。
* 下載新版本之後，就會發生間歇性的當機。

> [!NOTE]
> 自動更新的已知的問題可能會造成失敗的更新從 SSMA v8.1 v8.2。 如果您遇到這個錯誤，請下載新版本，並手動安裝它。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件。

## <a name="ssma-v81"></a>SSMA v8.1

V8.1 版的 SSMA for MySQL 被增強的目標式修正，專為改善品質和轉換的計量。

> [!NOTE]
> 自動更新的已知的問題可能會造成失敗的更新從 SSMA 8.0 版 v8.1。 如果您遇到這個錯誤，請下載新版本，並手動安裝它。

## <a name="ssma-v80"></a>SSMA v8.0

8\.0 版版的 SSMA for MySQL 被增強的目標式修正，旨在改善品質和轉換的計量。 此版本也提供了下列新功能：

* 支援**Azure SQL Database 受控執行個體**做為目標。 您現在可以建立新的專案目標 Azure SQL Database 受控執行個體：

  ![SQL DB MI 專案](../media/ssma-newproject-sqldbmi.png)

* 轉換後**修正 advisor**。 深入了解[此處](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)。

* 初步的資料庫/結構描述選取範圍。

  連接到來源時，使用者現在可以選取感興趣的資料庫/結構描述。 選取您要移轉的結構描述，會將儲存初始連線期間的時間，並改善整體的 SSMA 效能。

  ![SSMA 篩選物件](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

SSMA for MySQL v7.10 版本包含下列變更：

* 目標式的修正，旨在提供額外的安全性和隱私權保護，以符合全球需求的變更。
* 轉換函式名稱和引數清單之間的空格的修正。

## <a name="ssma-v79"></a>SSMA v7.9

SSMA for MySQL v7.9 版本包含下列變更：

* 目標式的修正，可改善品質和轉換的計量。
* 從 MySQL 移轉的空間資料類型，到 Azure SQL Database 的部分支援。
* 支援變更資料類型對應和專案的喜好設定的 SSMA 命令列中。
* 支援移轉使用 SQL Server Integration Services (SSIS) 資料。 轉換結構描述之後, 就可以建立 SSIS 封裝，透過右鍵操作功能表選項。
* SSMA 中的 [Azure SQL Database 連接] 對話方塊也已經改變指定完整的伺服器名稱。 在舊版的 SSMA，Azure SQL Database 的前置詞必須明確提及在專案設定。

## <a name="ssma-v78"></a>SSMA v7.8

SSMA for MySQL v7.8 版本包含下列變更：

* 變更專案設定中反白顯示的型別對應。
* 若要停用遙測的使用者的能力。

## <a name="ssma-v77"></a>SSMA v7.7

SSMA for MySQL v7.7 版本包含下列變更：

* 已改善品質和轉換計量的目標式修正與增強 SSMA for MySQL。
* 32 位元版本的 SSMA for MySQL 依據熱門的需求，已經恢復。 相較於先前的實作 （在之前 v7.4)，有兩個安裝程式套件，但它們無法並存安裝。 如此一來，您必須選擇您所擁有的最適當版本的連線元件為基礎。 一律最好是使用 64 位元版本，如果可能的話。
* 適用於 MySQL 的 SSMA 現在有 ODBC 連接字串連接模式，可讓您使用任何協力廠商 ODBC 驅動程式與 MySQL 相容。

## <a name="ssma-v76"></a>SSMA v7.6

已增強 v7.6 版的 SSMA for MySQL，改善品質和轉換計量的目標式修正與 SQL Server 2017 （公開預覽） 的支援。 在 Windows 和 Linux 上的 SQL Server 2017 支援處於公開預覽狀態，並不應該用於實際執行移轉。

## <a name="ssma-v75"></a>SSMA v7.5

增強 v7.5 版的 SSMA for MySQL 提供幾項改進，以確保更高的協助工具，方便殘障人士使用。

## <a name="ssma-v74"></a>SSMA v7.4

SSMA for MySQL v7.4 版本包含下列變更：

* **查詢逾時**選項已經可以使用在來源和目標結構描述物件探索期間。

    ![查詢逾時選項](../media/query-timeout_red.png)
* 品質和轉換的計量，而改善了目標式修正，根據客戶意見反應。

> [!IMPORTANT]
> .Net 4.5.2 是安裝 SSMA v7.4 的必要條件。 此外，開頭為 v7.4，32 位元版本的 SSMA 即將中止。

## <a name="ssma-v73"></a>SSMA v7.3

SSMA for MySQL v7.3 版本包含下列變更：

* 改善的品質和轉換度量目標式修正，根據客戶意見反應。
* SSMA 擴充性架構，透過下列項目公開：
  * 匯出至 SQL Server Data Tools (SSDT) 專案的功能。
    * 您現在可以從 SSMA 匯出結構描述指令碼，SSDT 專案。 您可以使用結構描述指令碼來進行其他的結構描述變更及部署您的資料庫。

      ![將儲存為 SSDT 專案命令](../media/export-schema-scripts_red.png)
  * 可供執行自訂轉換的 SSMA 的程式庫。
    * 您現在可以建構自訂的語法轉換和轉換先前未處理的 SSMA 可以處理的程式碼。
      * 在此部落格文章中，可指示如何建構自訂轉換器[擴充 SQL Server Migration Assistant 的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      * 下載範例專案進行轉換，從此[部落格文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)。

## <a name="ssma-v72"></a>SSMA v7.2

SSMA for MySQL v7.2 版本包含下列變更：

* 改善的品質和轉換度量目標式修正，根據客戶意見反應。
* 若要提供更好的資料點，來解決客戶問題，並改善 SSMA 的轉換率的遙測增強功能。

## <a name="ssma-v71"></a>SSMA v7.1

適用於 MySQL 的 SSMA 7.1 版發行版本包含下列變更：

* 在 Windows 和 Linux CTP1 上的 SQL Server 2017 現支援的目標平台進行移轉。 這項功能是在 technical preview 中，並允許結構描述和資料移動至目標 SQL server。
* SSMA 現在支援自動更新，以下載最新版本的 SSMA，因為它位於。
* SSMA 安裝二進位檔現在都是透過 Windows installer 套件檔案 (.msi) 提供。

## <a name="may-2016"></a>2016 年  
2016 年版的 SSMA for MySQL 包含下列變更：

* 已新增的支援 SQL Server 2016。
* 改進的剖析和解析程式。
* 已移除適用於.Net 2.0 的安裝程式檢查。
* 更新延伸模組組件相依性從.Net 3.5 到.Net 4.0。
* 適用於 MySql 的固定的預設 BigInt 型別對應。
* 已修正 儲存專案 」 和 SSMA 主控台的 開啟專案 命令。
* SSMA 主控台中修正 「 securepassword"命令。
* 已修正的初始載入的物件計數。
* 正在載入的固定的 MsSql 物件。
* 全域設定中已修正的 bug。

## <a name="march-2016"></a>2016 年 3 月

2016 年 3 月預覽版本的 SSMA for MySQL 會將 SQL Server 2016 中的移轉支援。 
  
## <a name="january-2016"></a>2016 年 1 月

2016 年 1 月維護版的 SSMA for MySQL 包含下列變更：  

* 新增的檢視至 SSMA (RFC 5706203) 的記錄功能表項目。  
* 已新增的遙測。  
  
## <a name="july-2014"></a>2014 年 7 月

2014 年 7 月版的 SSMA for MySQL 包含下列變更：  
  
* 改善的 Azure SQL DB 的程式碼轉換。 
* 延伸模組組件功能移至結構描述以支援 Azure SQL DB。  
* 效能改進測試針對具有超過 10 萬元的資料庫物件。  
* 處理大量物件的 UI 增強功能。  
* 反白顯示 「 已知 」 的 LOB 結構描述 （因此它們可以在轉換中應忽略）。  
* 轉換速度改善。  
* 顯示在 UI 中的物件計數。  
* 超過 25%的報表大小縮減。  
* 未剖析的建構的改良的錯誤訊息。  
  
## <a name="april-2014"></a>2014 年 4 月

2014 年 4 月版的 SSMA for MySQL 包含下列變更：  
  
* 已新增的 MS SQL Server 2014 的支援。  
* 關於轉換至 Azure 已經修正的 bug  
* 已修正的 IE 10 中的不可見的報表頁面相關的 bug。  
  
## <a name="july-2011"></a>2011 年 7 月

2011 年 7 月版的 SSMA for MySQL 包含下列變更：  
  
* 支援的限制轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"Denali"的位移。  
* 資料移轉期間報告改良的錯誤。  
  
## <a name="april-2011"></a>2011 年 4 月

2011 年 4 月版的 SSMA for MySQL 包含下列變更：  
  
* 可安裝的"SSMA for MySQL"，可支援單一[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005年[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008年[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"Denali"] 和 [Azure SQL。  
* 連線能力[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"Denali"。  
* 增強型的用戶端資料移轉引擎，支援平行移轉資料。  
* 改善的資料移轉效能與簡單和大量記錄復原模式。  
* SSMA for MySQL 主控台版本支援回溯相容性。 您可以開啟 SSMA v5.0 稍早的版本所建立的專案。  
* SSMA for MySQL v5.0 產品可以是會隨 SSMA 產品較舊版本中的並存 (SxS)。  
  
## <a name="july-2010"></a>2010 年 7 月

2010 年 7 月版的 SSMA for MySQL 包含下列功能：  
  
1. **使用者介面改善功能：**  
  
    * MySQL 資料庫物件的 「 SQL 模式 」 索引標籤  
    * MySQL 資料庫物件的 [設定] 索引標籤  
    * MySQL 資料表的 [資料] 索引標籤  
    * 在轉換和移轉 頁面更新的專案設定  
    * 在資料表層級的 [資料移轉設定]  
  
2. **連線到 MySQL 和 SQL Server 的增強功能：**  
  
    * 在 MySQL 中的 SSL 連線能力  
    * SQL Server 中的加密的連線  
  
3. **MySQL Metabase Explorer 的增強功能：**  
  
    * 正在載入所有的 MySQL 資料庫物件以及其個別的索引標籤。  
  
4. **物件轉換成的改進：**
  
    * 轉換 MySQL Metabase 物件-程序、 函數、 檢視、 觸發程序和陳述式。  
    * 在資料表中的空間資料類型的有限的支援。
    * 若要將 MySQL 函式轉換成 SQL Server 預存程序的選項  
    * 若要套用 SQL 模式和字元集對應物件轉換期間的選項  
  
5. **資料移轉的增強功能：**  
  
    * 使用伺服器端和用戶端資料移轉引擎的資料移轉支援  
    * 空間資料移轉支援  
    * 自訂的 SQL 資料表的資料移轉  
  
6. **SSMA for MySQL 主控台：**  
  
    * SSMA for MySQL 的支援主控台功能  
    * 指令碼層級互動的支援  
  
## <a name="january-2010"></a>2010 年 1 月

2010 年 1 月版的 SSMA for MySQL 是初始版本。 它包含下列功能： 
  
* 已新增的移轉，同時支援內部部署 SQL Server 和 Azure SQL。  
  
* **功能的快照集：** 結構描述和資料移轉的 MySQL 資料表/索引/條件約束。
