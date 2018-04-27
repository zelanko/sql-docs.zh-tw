---
title: SSMA for DB2 中最新消息 (DB2ToSQL) |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 03/01/2018
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: af743beadde9ae89984f5faa21cdccd9192693fb
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>SSMA for DB2 中最新消息 (DB2ToSQL)
本主題列出每個版本中的 DB2 變更 SSMA。  

## <a name="ssma-v77"></a>SSMA v7.7
V7.7 版的 SSMA for DB2 會包含下列變更：
- SSMA for DB2 已經增強，以改善品質和轉換的度量資訊的目標修正。
- 32 位元版本的 SSMA for DB2 根據需要常用，已經恢復。 相較於之前的實作 （前 v7.4)，有兩個安裝程式套件，但是它們無法並存安裝。 如此一來，您必須選擇最適當版本根據連接元件。 一律最好是盡可能使用 64 位元版本。

> [!IMPORTANT]
> SSMA v7.4 和更新版本，.Net 4.5.2 是安裝必要條件。

## <a name="ssma-v76"></a>SSMA v7.6
改善品質和轉換的度量資訊的目標修正程式與 SQL Server 2017 （公開預覽狀態） 的支援已經增強 v7.6 版的 SSMA for DB2。 支援在 Windows 和 Linux 上的 SQL Server 2017 是公開預覽狀態，而且不應該用於實際執行移轉。

> [!IMPORTANT]
> SSMA v7.4 和更新版本，.Net 4.5.2 為安裝必要元件，而 32 位元版本的工具已停用。

## <a name="ssma-v75"></a>SSMA v7.5
V7.5 版的 SSMA for DB2 已經增強，以確保行動不便人士更大的存取範圍的數個增強功能。

> [!IMPORTANT]
> .Net 4.5.2 是安裝 SSMA v7.5 的必要條件。 此外，開頭 v7.4，32 位元版本的 SSMA 會停止。

## <a name="ssma-v74"></a>SSMA v7.4
V7.4 版的 SSMA for DB2 會包含下列變更：
- **查詢逾時**選項現在時仍可使用在來源和目標結構描述物件探索。
![查詢逾時選項](../media/query-timeout_red.png)

- 品質和轉換的度量，而改善了目標的修正程式，根據客戶的意見反應。

> [!IMPORTANT]
> .Net 4.5.2 是安裝 SSMA v7.4 的必要條件。 此外，開頭 v7.4，32 位元版本的 SSMA 會停止。

## <a name="ssma-v73"></a>SSMA v7.3
V7.3 版的 SSMA for DB2 會包含下列變更：
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
V7.2 版的 SSMA for DB2 會包含下列變更：
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
2016 年版的 SSMA for DB2 會包含下列變更：  

-  已新增的支援 SQL Server 2016。
-  已新增到 SQL Server 記憶體中和 hekaton 功能 DB2 記憶體中和一般資料表的轉換。
-  新增的轉換 DB2 存取控制 SQL Server 原則物件 （for DB2 的資料列層級安全性）。
-  加入至 SQL Server 的時態表的 DB2 系統建立版本資料表的轉換。
-  改善的 DB2 剖析和解析程式。
-  移除安裝程式檢查適用於.Net 2.0。
-  從 Db2 安裝程式中移除不必要的 *.dll。
-  修正 儲存專案 」 以及 「 開啟專案 」 SSMA 主控台命令。
-  SSMA 主控台的固定"securepassword"命令。
-  已修正的初始載入的物件計數。
-  通用設定 中修正的 bug。
  
## <a name="march-2016"></a>2016 年 3 月  
2016 年 3 月預覽版本的 SSMA for DB2 會包含下列變更：  
  
-  移轉至 SQL Server 2016 所加入的支援。  
  
## <a name="january-2016"></a>2016 年 1 月  
2016 年 1 月維護版的 SSMA for DB2 會包含下列變更：  
  
-  已新增的支援的標準函式。  
-  修正 DB2 剖析器錯誤。  
-  固定的 DB2 v9 zOS 支援 (RFC 5690920)。  
-  固定的 DB2 無法解析在轉換期間的識別項錯誤。  
-  加入的檢視要 SSMA (建議 RFC 5706203) 的記錄檔 功能表項目。  
-  加入的遙測。
  
## <a name="november-2014"></a>2014 年 11 月  
2014 年 11 月版的 SSMA for DB2 是早的版本。
