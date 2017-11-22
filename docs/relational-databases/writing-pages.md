---
title: "寫入分頁 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: relational-databases-misc
ms.reviewer: 
ms.suite: sql
ms.technology: server-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: pages
ms.assetid: 409c8753-03c4-436d-839c-6a5879971551
caps.latest.revision: "2"
author: pmasl
ms.author: pelopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e116782bb7c78f69a1d7c90755e746e4587d4426
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="writing-pages"></a>寫入分頁
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[ssDE](../includes/ssde-md.md)] 執行個體中的 I/O 包括邏輯和實體寫入。 修改緩衝快取內分頁中的資料時，即會發生邏輯寫入。 將分頁從 [緩衝快取](../relational-databases/memory-management-architecture-guide.md) 寫入磁碟時，即會發生實體寫入。

修改緩衝快取中的分頁時，不會將其立即寫回磁碟，而是將該分頁標示為「中途」。 這表示在實際寫入磁碟之前，可以多次邏輯寫入頁面。 每次邏輯寫入時，都會有交易記錄插入至記載修改的記錄快取中。 記錄檔記錄必須在關聯的中途分頁從緩衝區快取移除而寫入至磁碟之前，先寫入磁碟中。 SQL Server 會使用稱為預寫記錄的技術，可防止在將相關聯的記錄檔記錄寫入磁碟之前，先寫入中途分頁。 這是復原管理員正確運作的先決條件。 如需詳細資訊，請參閱 [預先寫入交易記錄](../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)。

下圖顯示寫入已修改資料頁的程序。

![Writing_Pages](../relational-databases/media/writing-pages.gif)

緩衝區管理員寫入頁面時，會搜尋可併入單一累積寫出作業的相鄰中途分頁。 相鄰頁面有連續的頁面識別碼，而且來自相同的檔案；頁面在記憶體中不一定是連續的。 搜尋會同時向前、後兩個方向進行，直到下列其中一個事件發生為止：

 * 非中途頁面 (已寫入磁碟的頁面)。
 * 已經找到 32 個頁面。
 * 找到尚未在記錄中排清記錄序號 (LSN) 的中途分頁。
 * 找到無法立即閂鎖的頁面。

如此一來，可以利用單一累積寫出作業將整組頁面寫入磁碟。 

就在寫入頁面之前，資料庫中指定的頁面保護格式會加入至頁面。 如果加入的是損毀頁保護，則必須針對 I/O 以獨佔方式鎖住該分頁。 這是因為損毀頁保護會修改頁面，使得任何其他執行緒都不宜讀取。 如果加入的是總和檢查碼頁面保護，或者資料庫未使用頁面保護，則以 UP (更新) 閂鎖來鎖定頁面的 I/O。 此閂鎖會防止其他人在寫入期間修改頁面，但是仍允許讀取器使用它。 如需磁碟 I/O 分頁保護選項的詳細資訊，請參閱 [緩衝區管理](../relational-databases/memory-management-architecture-guide.md)。

中途分頁會透過下列三種方法之一寫入磁碟： 

* 延遲寫入   
 延遲寫入器是一個系統處理序，會從緩衝快取移除不常使用的頁面以持續提供可用的緩衝區空間。 中途分頁會首先寫入磁碟。 

* 急切寫入   
 急切寫入處理序會寫入與非記錄作業 (例如大量插入與選取插入) 相關聯的中途資料頁。 此處理序允許建立頁面與寫入新頁面的作業平行進行。 也就是說，呼叫作業不需要等到整個作業完成，即可將頁面寫入磁碟。

* 檢查點   
 檢查點處理序會定期掃描緩衝快取，檢查是否有內含來自指定資料庫之頁面的緩衝區，並將所有中途分頁寫入磁碟。 藉由建立一個點來確保所有中途分頁都已寫入磁碟中，檢查點可讓稍後的復原節省時間。 使用者可以使用 CHECKPOINT 命令來要求檢查點作業，或者也可以由 [!INCLUDE[ssDE](../includes/ssde-md.md)] 根據自最後一個檢查點以來所使用的記錄空間數量及經過的時間，自動產生檢查點。 此外，檢查點還會在發生特定活動時產生。 例如，從資料庫加入或移除資料或記錄檔時，或者在停止 SQL Server 的執行個體時。 如需詳細資訊，請參閱 [檢查點與記錄檔的使用中部份](../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)。

延遲寫入、急切寫入和檢查點處理序不會等待 I/O 作業完成。 這些處理序一律使用非同步 (或重疊) I/O，並繼續執行其他工作，稍後才檢查 I/O 是否成功。 這可讓 SQL Server 為適當的工作提供最多的 CPU 和 I/O 資源。

## <a name="see-also"></a>另請參閱
[分頁與範圍架構指南](../relational-databases/pages-and-extents-architecture-guide.md)   
 [讀取分頁](../relational-databases/reading-pages.md)
