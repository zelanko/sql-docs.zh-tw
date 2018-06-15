---
title: SSMA for MySQL (MySQLToSql) 中最新消息 |Microsoft 文件
ms.prod: sql
ms.custom: ''
ms.date: 03/01/2018
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
caps.latest.revision: 21
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d818a1ce31d752898d5d1ebde5a27addbedd91ad
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34776674"
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>SSMA for MySQL (MySQLToSql) 中最新消息
本主題列出每個版本中的 MySQL 變更 SSMA。 

## <a name="ssma-v77"></a>SSMA v7.7
SSMA for MySQL 的 v7.7 版本包含下列變更：
- SSMA for MySQL 已經增強，以改善品質和轉換的度量資訊的目標修正。
- 32 位元版本的 SSMA for MySQL 根據需要常用，已經恢復。 相較於之前的實作 （前 v7.4)，有兩個安裝程式套件，但是它們無法並存安裝。 如此一來，您必須選擇最適當版本根據連接元件。 一律最好是盡可能使用 64 位元版本。
- SSMA for MySQL 現在具有 ODBC 連接字串連接模式，可讓您使用任何協力廠商 ODBC 驅動程式與 MySQL 相容。

> [!IMPORTANT]
> SSMA v7.4 和更新版本，.Net 4.5.2 是安裝必要條件。

## <a name="ssma-v76"></a>SSMA v7.6
V7.6 版的 SSMA for MySQL 已經增強，改善品質和轉換的度量資訊的目標修正程式與 SQL Server 2017 （公開預覽狀態） 的支援。 支援在 Windows 和 Linux 上的 SQL Server 2017 是公開預覽狀態，而且不應該用於實際執行移轉。

> [!IMPORTANT]
> SSMA v7.4 和更新版本，.Net 4.5.2 為安裝必要元件，而 32 位元版本的工具已停用。

## <a name="ssma-v75"></a>SSMA v7.5
V7.5 版的 SSMA for MySQL 已經增強，以確保行動不便人士更大的存取範圍的數個增強功能。

> [!IMPORTANT]
> .Net 4.5.2 是安裝 SSMA v7.5 的必要條件。 此外，開頭 v7.4，32 位元版本的 SSMA 會停止。

## <a name="ssma-v74"></a>SSMA v7.4
SSMA for MySQL 的 v7.4 版本包含下列變更：
- **查詢逾時**選項現在時仍可使用在來源和目標結構描述物件探索。
![查詢逾時選項](../media/query-timeout_red.png)
- 品質和轉換的度量，而改善了目標的修正程式，根據客戶的意見反應。

> [!IMPORTANT]
> .Net 4.5.2 是安裝 SSMA v7.4 的必要條件。 此外，開頭 v7.4，32 位元版本的 SSMA 會停止。 

## <a name="ssma-v73"></a>SSMA v7.3
SSMA for MySQL 的 v7.3 版本包含下列變更：
- 改善的品質和轉換的度量根據客戶的意見反應目標的修正程式。
- 透過下列項目公開 SSMA 擴充性架構：
  - 匯出至 SQL Server Data Tools (SSDT) 專案的功能。
    -   您現在可以在 SSDT 專案，從 SSMA 匯出結構描述指令碼。 您可以使用結構描述指令碼來進行額外的結構描述變更及部署您的資料庫。
![將儲存為 SSDT 專案命令](../media/export-schema-scripts_red.png)
  - 可供 SSMA 執行自訂轉換執行的程式庫。
    - 您現在可以建構自訂語法轉換和 SSMA 先前未處理的轉換可以處理的程式碼。
      - 這個部落格文章，指示如何建構自訂轉換子可用[擴充 SQL Server 移轉小幫手的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      - 轉換的範例專案可以是下載此[部落格文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)。

## <a name="ssma-v72"></a>SSMA v7.2
SSMA for MySQL 的 v7.2 版本包含下列變更：
- 改善的品質和轉換的度量根據客戶的意見反應目標的修正程式。
- 遙測增強功能提供更好的資料點，來解決客戶問題，並改善 SSMA 的轉換比率。

## <a name="ssma-v71"></a>SSMA 7.1 版
SSMA for Access 的 7.1 版發行版本包含下列變更：
- 在 Windows 和 Linux CTP1 上的 SQL Server 2017 已移轉的支援的目標平台。 此功能是 technical preview 中，並可讓結構描述和資料移動到目標 SQL 伺服器。
- SSMA 現在支援自動更新，以下載最新版本的 SSMA，如有的話。
- SSMA 可安裝二進位檔現在都是透過 Windows installer 封裝檔案 (.msi) 提供。

**資源**

[擴充 SQL Server 移轉小幫手的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[評估並將資料從非 Microsoft 資料平台移轉到 SQL Server *（與 Oracle 範例）*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>2016 年  
SSMA for MySQL 的 2016 年版本包含下列變更:。

-  已新增的支援 SQL Server 2016。
-  改良的剖析和解析程式。
-  移除安裝程式檢查適用於.Net 2.0。
-  更新擴充功能組件相依性從.Net 3.5.net 4.0。
-  固定的預設用於 MySql 的 BigInt typemapping。
-  修正 儲存專案 」 以及 「 開啟專案 」 SSMA 主控台命令。
-  SSMA 主控台的固定"securepassword"命令。
-  已修正的初始載入的物件計數。
-  載入的固定的 MsSql 物件。
-  通用設定 中修正的 bug。
 
## <a name="march-2016"></a>2016 年 3 月  
2016 年 3 月 preview 版的 SSMA for MySQL 包含下列變更：  
  
-  移轉至 SQL Server 2016 所加入的支援。 
  
## <a name="january-2016"></a>2016 年 1 月  
2016 年 1 月維護版的 SSMA for MySQL 包含下列變更：  
  
-  加入的檢視要 SSMA (建議 RFC 5706203) 的記錄檔 功能表項目。  
-  加入的遙測。  
  
## <a name="july-2014"></a>2014 年 7 月  
2014 年 7 月版的 SSMA for MySQL 包含下列變更：  
  
-  改善的 Azure SQL DB 程式碼轉換。 
-  延伸模組組件的功能移至結構描述，以支援 Azure SQL DB。  
-  包含超過 10k 之資料庫的物件測試的效能改進。  
-  處理大量物件的 UI 增強功能。  
-  反白顯示 「 已知 」 的 LOB 結構描述 （因此可在轉換中予以忽略）。  
-  轉換速度改善。  
-  顯示在 UI 中的物件計數。  
-  報表大小縮減超過 25%。  
-  未剖析建構的改良的錯誤訊息。  
  
## <a name="april-2014"></a>2014 年 4 月  
2011 年 7 月版的 SSMA for MySQL 包含下列變更：  
  
-  已新增的支援 MS SQL Server 2014。  
-  已修正的 bug，關於轉換至 Azure  
-  關於不可見的報表頁面在 IE 10 中已修正的 bug。  
  
## <a name="july-2011"></a>2011 年 7 月  
2011 年 7 月版的 SSMA for MySQL 包含下列變更：  
  
-   支援的限制，以轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"的位移。  
-   在資料遷移期間報告改良的錯誤。  
  
## <a name="april-2011"></a>2011 年 4 月  
2011 年 4 月版的 SSMA for MySQL 包含下列變更：  
  
-   單一 「 SSMA for MySQL 的 」，可支援可安裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005 年[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2008年[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"和 Azure SQL。  
-   連線能力[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"。  
-   增強型的用戶端資料移轉引擎，支援平行的資料移轉。  
-   提升的資料移轉效能簡單與大量記錄復原模式。  
-   SSMA for MySQL 主控台版本支援回溯相容性。 您可以開啟 SSMA v5.0 稍早的版本所建立的專案。  
-   SSMA for MySQL v5.0 產品可以安裝與舊版本的 SSMA 產品的並存 (SxS)。  
  
## <a name="july-2010"></a>2010 年 7 月  
2010 年 7 月版的 SSMA for MySQL 包含下列功能：  
  
1.  **使用者介面的增強功能：**  
  
    -   MySQL 資料庫物件的 「 SQL 模式 」 索引標籤  
    -   MySQL 資料庫物件的 [設定] 索引標籤  
    -   MySQL 資料表的 [資料] 索引標籤  
    -   轉換和移轉頁面中的已更新的專案設定  
    -   在資料表層級的 [資料移轉設定]  
  
2.  **連接到 MySQL 及 SQL Server 的增強功能：**  
  
    -   在 MySQL 的 SSL 連線  
    -   SQL Server 中的加密的連線  
  
3.  **MySQL Metabase Explorer 的增強功能：**  
  
    -   正在載入的所有 MySQL 資料庫物件和其各自的索引標籤。  
  
4.  **物件轉換的增強功能：**  
  
    -   轉換的 MySQL Metabase 物件 – 程序、 函數、 檢視、 觸發程序和陳述式。  
    -   在資料表中的空間資料類型的有限的支援。  
    -   選項可將 MySQL 函式轉換成 SQL Server 預存程序  
    -   若要套用 SQL 模式和字元集對應物件轉換期間的選項  
  
5.  **資料移轉的增強功能：**  
  
    -   使用伺服器端和用戶端資料移轉引擎的資料移轉支援  
    -   空間資料移轉支援  
    -   自訂 SQL 資料表的資料移轉  
  
6.  **SSMA for MySQL 主控台：**  
  
    -   SSMA for MySQL 針對支援主控台功能  
    -   指令碼層級互動的支援  
  
## <a name="january-2010"></a>2010 年 1 月  
2010 年 1 月版的 SSMA for MySQL 是早的版本。 它包含下列功能：  
  
-   已新增的支援同時移轉內部部署 SQL Server 和 Azure SQL。  
  
-   **功能的快照集：** 結構描述和資料移轉的 MySQL 資料表/索引/條件約束。
