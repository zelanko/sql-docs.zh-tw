---
title: SQL Server 的 Databases 物件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Databases object
- SQLServer:Databases
- Availability Groups [SQL Server], performance counters
ms.assetid: a7f9e7d4-fff4-4c72-8b3e-3f18dffc8919
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b4c0c7a5626f3eb48509d7a4cfbf239f7cb931da
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63250644"
---
# <a name="sql-server-databases-object"></a>SQL Server、Databases 物件
  SQL Server 中的 **SQLServer:Databases** 物件提供計數器，可用來監視大量複製作業、備份和還原輸送量以及交易記錄活動。 監視交易和交易記錄檔，可以判斷資料庫中有多少使用者活動，以及交易記錄檔有多滿。 使用者活動量可用來判斷資料庫的效能，並且會影響記錄檔大小、鎖定和複寫。 監視低階記錄檔活動，則可量測使用者活動和資源使用量，以協助您找出效能瓶頸。  
  
 您可同時監視 **Databases** 物件的多個執行個體，每個執行個體都代表一個資料庫。  
  
 下表描述 SQL Server **Databases** 計數器。  
  
|SQL Server Databases 計數器|描述|  
|-----------------------------------|-----------------|  
|**Active Transactions**|資料庫的使用中交易數。|  
|**備份/還原輸送量/秒**|每秒的資料庫備份和還原作業之讀取/寫入輸送量。 例如，您可以測量同時使用更多個備份裝置或是使用了更快的裝置時，資料庫備份作業的效能改變情形。 資料庫備份或還原作業的輸送量，可讓您判斷備份和還原作業的進度和效能。|  
|**大量複製資料列數/秒**|每秒大量複製 (Bulk Copy) 的資料列數。|  
|**大量複製輸送量/秒**|每秒大量複製的資料量 (以 KB 為單位)。|  
|**認可資料表專案**|資料庫認可資料表之記憶體中部分的大小。 如需詳細資訊，請參閱 [sys.dm_tran_commit_table &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/change-tracking-sys-dm-tran-commit-table)。|  
|**資料檔案大小（KB）**|資料庫內的所有資料檔案總計大小 (以 KB 為單位)，包含任何自動的成長。 監視此計數器很有用，例如可決定 **tempdb**的正確大小。|  
|**DBCC 邏輯掃描位元組數/秒**|資料庫主控台命令 (DBCC) 每秒的邏輯讀取掃描位元組數。|  
|**記錄快取點擊率**|記錄檔快取所滿足的記錄檔快取讀取百分比。|  
|**記錄檔快取讀取/秒**|每秒透過記錄檔管理員快取所執行的讀取數。|  
|**記錄檔大小（KB）**|資料庫內所有交易記錄檔的總計大小 (以位元組為單位)。|  
|**已使用的記錄檔大小（KB）**|資料庫中所有記錄檔的總計使用大小。|  
|**記錄檔排清等候時間**|排清記錄檔的等候時間總計 (以毫秒為單位)。 在 AlwaysOn 次要資料庫上，此值表示記錄檔記錄強行寫入磁碟的等候時間。|  
|**記錄排清等待/秒**|每秒鐘等候記錄檔排清的認可數。|  
|**記錄檔排清寫入時間（毫秒）**|執行在最後一筆記錄中完成之記錄檔排清寫入的時間 (以毫秒為單位)。|  
|**記錄檔排清/秒**|每秒的記錄檔排清數目。|  
|**記錄檔 Growths**|資料庫之交易記錄檔的擴大總次數。|  
|**記錄壓縮**|資料庫之交易記錄縮小的總次數。|  
|**記錄集區快取遺漏/秒**|記錄檔區塊無法在記錄檔集區中使用的要求數目。 「記錄集區」** 是交易記錄的記憶體中快取。 此快取是用來最佳化記錄的讀取，以便進行復原、交易複寫、回復和 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]。|  
|**記錄集區磁片讀取/秒**|由記錄檔集區發出來提取記錄檔區塊的磁碟讀取數目。|  
|**記錄集區要求數/秒**|記錄檔集區處理的記錄檔區塊要求數目。|  
|**記錄檔截斷**|交易記錄檔被壓縮的次數。|  
|**使用的記錄百分比**|使用中的記錄檔空間百分比。|  
|**正在進行複寫。暫止個交易**|標示成複寫、但未傳送到散發資料庫的發行集資料庫內的交易記錄檔之交易數。|  
|**Repl. Trans. Rate**|每秒自發行集資料的交易記錄檔讀取並傳送至散發資料庫的交易數。|  
|**壓縮資料移動位元組/秒**|經由自動壓縮作業或是 DBCC SHRINKDATABASE 或 DBCC SHRINKFILE 陳述式移動的每秒資料量。|  
|**追蹤的交易數/秒**|資料庫的認可資料表中記錄的已認可交易數目。|  
|**交易數/秒**|每秒針對資料庫啟動的交易數。<br /><br /> **每秒交易**數不會計算僅限 XTP 交易（由原生編譯的預存程式啟動的交易）。|  
|**寫入交易數/秒**|上一秒寫入資料庫並認可的交易數目。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用量 &#40;系統監視器&#41;](monitor-resource-usage-system-monitor.md)   
 [SQL Server、資料庫複本](sql-server-database-replica.md)  
  
  
