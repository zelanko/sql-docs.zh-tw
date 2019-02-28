---
title: 什麼是適用於 SAP ASE (SybaseToSQL) 的 SSMA 的新功能 |Microsoft Docs
ms.custom: ''
ms.date: 02/27/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2345fd2f5a30c8eba610a49524c058ebf1cfae5f
ms.sourcegitcommit: 2ab79765e51913f1df6410f0cd56bf2a13221f37
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/27/2019
ms.locfileid: "56955949"
---
# <a name="whats-new-in-ssma-for-sap-ase-sybasetosql"></a>什麼是適用於 SAP ASE (SybaseToSQL) 的 SSMA 的新功能
本文章列出 SQL Server Migration Assistant (SSMA) 的每個版本中的 SAP ASE (先前稱為 SSMA for Sybase) 變更。 

## <a name="ssma-v80"></a>SSMA v8.0
SSMA for Access 8.0 版發行已經過增強，以提供目標式的修正，旨在改善品質和轉換的計量。 此外，此版本提供了下列新功能：

* 支援**Azure SQL Database 受控執行個體**做為目標。 您現在可以建立新的專案目標 Azure SQL Database 受控執行個體：

    ![SQL DB MI 專案](../media/ssma-newproject-sqldbmi.png)

*   轉換後**修正 advisor**。 深入了解[此處](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)。

*   初步的資料庫/結構描述選取範圍。

    連接到來源時，使用者現在可以選取感興趣的資料庫/結構描述。 選取您要移轉的結構描述，會將儲存初始連線期間的時間，並改善整體的 SSMA 效能。

    ![SSMA 篩選物件](../media/ssma-filter-objects.png)

> [!IMPORTANT]
> 使用 SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件。

## <a name="ssma-v710"></a>SSMA v7.10
適用於 SAP ASE v7.10 版的 SSMA 的增強提供目標式修正，旨在提供額外的安全性和隱私權保護，以符合全球需求的變更。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件。

## <a name="ssma-v79"></a>SSMA v7.9
適用於 SAP ASE v7.9 版的 SSMA 包含下列變更：
- 目標式的修正，可改善品質和轉換的計量。
- 支援變更資料類型對應和專案的喜好設定的 SSMA 命令列中。
- 支援移轉使用 SQL Server Integration Services (SSIS) 資料。 轉換結構描述之後, 就可以建立 SSIS 封裝，透過右鍵操作功能表選項。
- SSMA 中的 [Azure SQL Database 連接] 對話方塊也已經改變指定完整的伺服器名稱。 在舊版的 SSMA，Azure SQL Database 的前置詞必須明確提及在專案設定。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件。

## <a name="ssma-v78"></a>SSMA v7.8
適用於 SAP ASE v7.8 版的 SSMA 包含下列變更：
- 專案設定中的反白顯示的變更型別對應。
- 提供可讓使用者以停用遙測。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件。

## <a name="ssma-v77"></a>SSMA v7.7
適用於 SAP ASE v7.7 版的 SSMA 包含下列變更：
- SSMA 適用於 SAP ASE 已經過加強，以改善品質和轉換計量的目標式修正。
- 32 位元版本的 SSMA for SAP ASE 依據熱門的需求，已經恢復。 相較於先前的實作 （在之前 v7.4)，有兩個安裝程式套件，但它們無法並存安裝。 如此一來，您必須選擇您所擁有的最適當版本的連線元件為基礎。 一律最好是使用 64 位元版本，如果可能的話。

> [!IMPORTANT]
> 使用 SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件。

## <a name="ssma-v76"></a>SSMA v7.6
適用於 SAP ASE v7.6 版的 SSMA 包含下列變更：
- SSMA 適用於 SAP ASE 已經過加強，改善品質和轉換計量的目標式修正與 SQL Server 2017 （公開預覽） 的支援。 在 Windows 和 Linux 上的 SQL Server 2017 支援處於公開預覽狀態，並不應該用於實際執行移轉。
- 適用於 SAP ASE 的 SSMA 已更新以支援 Sybase 函式的轉換。

> [!IMPORTANT]
> SSMA v7.4 和更新版本，.Net 4.5.2 可安裝的必要條件，與 32 位元版本的工具已停用。

## <a name="ssma-v75"></a>SSMA v7.5
適用於 SAP ASE v7.5 版的 SSMA 包含下列變更：
-   增強的幾項改進，以確保更高的協助工具，方便殘障人士使用。
-   更新以支援建立或取代的語法。

> [!IMPORTANT]
> .Net 4.5.2 是安裝 SSMA v7.5 的必要條件。 此外，開頭為 v7.4，32 位元版本的 SSMA 即將中止。  

## <a name="ssma-v74"></a>SSMA v7.4
SSMA for Sybase 的 v7.4 版本包含下列變更：
- **查詢逾時**選項已經可以使用在來源和目標結構描述物件探索期間。
![查詢逾時選項](../media/query-timeout_red.png)
- 品質和轉換的計量，而改善了目標式修正，根據客戶意見反應。

> [!IMPORTANT]
> .Net 4.5.2 是安裝 SSMA v7.4 的必要條件。 此外，開頭為 v7.4，32 位元版本的 SSMA 即將中止。  

## <a name="ssma-v73"></a>SSMA v7.3
SSMA for Sybase 的 v7.3 版本包含下列變更：
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
SSMA for Sybase 的 v7.2 版本包含下列變更：
- 改善的品質和轉換度量目標式修正，根據客戶意見反應。
- 若要提供更好的資料點，來解決客戶問題，並改善 SSMA 的轉換率的遙測增強功能。

## <a name="ssma-v71"></a>SSMA v7.1
SSMA for Access v7.1 版本包含下列變更：
- 在 Windows 和 Linux CTP1 上的 SQL Server 2017 現支援的目標平台進行移轉。 這項功能處於技術預覽狀態，並支援結構描述和資料移動至目標 SQL server。
- SSMA 現在支援自動更新，以下載最新版本的 SSMA，因為它位於。
- SSMA 安裝二進位檔現在都是透過 Windows installer 套件檔案 (.msi) 提供。

**資源**

[擴充 SQL Server Migration Assistant 的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[評估並將資料從非 Microsoft 資料平台移轉至 SQL Server *（含 Oracle 範例）*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>2016 年  
2016 年版的 SSMA for Sybase 包含下列變更：  

-  已新增的支援 SQL Server 2016。
-  已移除適用於.Net 2.0 的安裝程式檢查。
-  更新延伸模組組件相依性從.Net 3.5 到.Net 4.0。
-  已修正 儲存專案 」 和 SSMA 主控台的 開啟專案 命令。
-  SSMA 主控台中修正 「 securepassword"命令。
-  已修正的初始載入的物件計數。
-  全域設定中已修正的 bug。

## <a name="march-2016"></a>2016 年 3 月  
2016 年 3 月預覽版本的 SSMA for Sybase 包含下列變更：  
  
-  新增的移轉至 SQL Server 2016 的支援。  
  
## <a name="january-2016"></a>2016 年 1 月  
2016 年 1 月維護版的 SSMA for Sybase 包含下列變更：  
  
-  新增的檢視至 SSMA (RFC 5706203) 的記錄功能表項目。  
-  已新增的遙測。 
  
## <a name="july-2014"></a>2014 年 7 月  
SSMA for Sybase 的 2014 年 7 月版本包含下列變更：  
  
-  改善的 Azure SQL DB 的程式碼轉換。  
-  移到 結構描述，以支援 Azure SQL DB 的延伸模組組件功能。  
-  新增的效能改進測試針對具有超過 10 萬元的資料庫物件。  
-  已新增的 UI 增強功能來處理大量的物件。  
-  新增 （讓他們可以在轉換中應忽略），反白顯示 「 已知 」 的 LOB 結構描述的能力。  
-  新增轉換速度改善。  
-  新增在 UI 中顯示物件計數的功能。 
-  減少的報表的大小超過 25%。  
-  未剖析的建構的改良的錯誤訊息。  
  
## <a name="april-2014"></a>2014 年 4 月  
SSMA for Sybase 的 2014 年 4 月版本包含下列變更：  
  
-   已新增的 MS SQL Server 2014 的支援。  
-   關於轉換至 Azure 已經修正的 bug。  
-   已修正的 IE 10 中的不可見的報表頁面相關的 bug。  
  
## <a name="january-2012"></a>2012 年 1 月  
SSMA for Sybase 的 2012 年 1 月版本包含下列變更：  
  
-   已新增的支援回復觸發程序轉換。  
-   轉換提供修正@ROWCOUNT和 @@ERROR中相同的 SET 陳述式。  
  
## <a name="july-2011"></a>2011 年 7 月  
SSMA for Sybase 的 2011 年 7 月版本包含下列變更：  
  
-   資料移轉期間報告改良的錯誤。  
  
## <a name="april-2011"></a>2011 年 4 月  
SSMA for Sybase 的 2011 年 4 月版本包含下列變更：  
  
-   彙總支援的 「 SSMA for Sybase 」 產品[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005年[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008年[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"Denali"] 和 [Azure SQL。  
-   已新增支援連接，並移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]"Denali"。  
-   加入新的功能，可將轉換，將 Sybase 資料庫移轉至 Azure SQL。  
-   增強型的用戶端資料移轉引擎，支援平行移轉資料。  
-   改善的資料移轉效能與簡單和大量記錄復原模式。  
-   新增的功能，才能正確轉換，並區分大小寫的 Sybase 資料庫移轉至區分大小寫的 SQL Server。  
-   已新增的支援的 SQL Server 的 ANSI 聯結陳述式的 Sybase ASE 非 ANSI 聯結陳述式轉換已經過擴充，若要刪除及 UPDATE 陳述式。  
-   提供其他連接選項連接到 Sybase ASE 使用 Sybase ASE ODBC 提供者和 Sybase ASE ADO.Net 提供者的伺服器。  
-   移除對個別的資料庫呼叫的相依性**SysDB**，其中包含 Sybase 模擬函式 （安裝延伸模組套件的一部分）。  
-   新增的功能上安裝 SSMA for Sybase 延伸模組套件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]叢集。  
-   已新增的較早版本的 SSMA （v4.0 和 4.2 版） 所建立之專案的回溯相容性。  
-   已新增使用較舊版本的 SSMA （v4.0 和 4.2 版） 安裝 SSMA for Sybase v5.0 產品的並存 (SxS) 的能力。  
  
## <a name="july-2010"></a>2010 年 7 月  
SSMA for Sybase 的 2010 年 7 月版本包含下列變更：  
  
-   已新增的支援移轉至 SQL Server 2008 R2。  
-   加入新的 SSMA 主控台應用程式的命令列執行。  
-   已新增的支援使用伺服器端和用戶端資料移轉引擎的資料移轉。  
-   已新增的支援在資料移轉的 「 自訂選取 」 陳述式。  
-   從 Sybase ASE 15.0.3 和 15.5 移轉新增的支援。  
  
## <a name="june-2008"></a>2008 年 6 月  
2008 年 6 月版的 SSMA for Sybase 包含下列變更：  
  
-   已新增的 SSMA Tester，這會自動測試資料庫物件轉換和 SSMA 所做的資料移轉。 所有 SSMA 的移轉步驟都完成之後，使用 SSMA 軟體測試人員確認已轉換的物件執行相同的方式，而且所有的資料已正確移轉。  
-   已新增的每個 SQL 轉換。 使用者現在可以指定暫存資料表 （和其他物件） 來轉換每個來源程序的宣告。  
-   加入的物件轉換中的改進：  
    -   聯結修訂的轉換。  
    -   彙總及非彙總而不需要/群組 by 子句。  
    -   IDENTITY 函式使用 SELECT INTO 陳述式。  
    -   叢集條件約束和索引上的資料僅鎖定。  
    -   SELECT INTO 所建立的暫存資料表。  
    -   條件約束 / 編製索引的暫存資料表。  
    -   新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援 2008 datetime 類型。  
    -   Sybase 15.0 連線和資料型別支援。  
  
## <a name="may-2007"></a>2007 年 5 月  
SSMA for Sybase 的 2007 年版本包含下列變更：  
  
-   新增能力以儲存專案時，更快載入資料庫內容。  
-   已新增的支援 SQL Server 中的使用者輸入註解格式 SQL 模式。  
-   已新增的進步物件轉換的詳細資訊。  
  
此版本未更新的說明檔。 如需詳細資訊，請參閱本文稍後的文件提示 > 一節。  
  
## <a name="november-2006"></a>2006 年 11 月  
2006 年 11 月版的 SSMA for Sybase 包含下列變更：  
  
-   新增新的全域設定：  
    -   您可以選擇在編輯器視窗中顯示行號。  
    -   您可以設定 SSMA 提示來取代重複的物件，或一律或永遠不會取代重複的物件結構描述轉換期間。  
-   加入新的轉換選項可讓您設定 SSMA 如何處理下列情況：  
    -   CAST 或 CONVERT 陳述式，其中包含二進位字串。  
    -   檢查的等號比較運算式中的 null 值。  
    -   Proxy 的資料表。  
    -   使用者訊息 RAISERROR 的錯誤號碼。  
    -   包含無法解析識別項的 UPDATE 陳述式。  
-   加入新的移轉選項，可讓您指定 SSMA 應該如何處理以外的日期[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日期範圍。  
-   新增**格式化 SQL**上設定**SQL**索引標籤上，將格式化的程式碼，以改善可讀性。  
-   Bug 修正，包括：  
    -   SSMA 現在將鎖定資料表*資料表*IN {共用 |藉由將後續的 SELECT 查詢資料表的 TABLOCK 或 TABLOCKX 提示的獨占} 模式陳述式。  
    -   當字元運算式中使用二進位類型現在已新增必要的轉換 （cast）。  
    -   記憶體和效能改進。  
  
## <a name="july-2006"></a>2006 年 7 月  
2006 年 7 月版的 SSMA for Sybase 是最早的版本。  
  
## <a name="see-also"></a>另請參閱  
[開始使用 SSMA for Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
