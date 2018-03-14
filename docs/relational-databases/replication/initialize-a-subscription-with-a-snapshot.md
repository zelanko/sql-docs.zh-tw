---
title: "使用快照集初始化訂閱 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 77a9ade2-cdc0-4ae9-a02d-6e29d7c2ada0
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3749a2de953dd43419ca9ec6186817b62bfc5fa6
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="initialize-a-subscription-with-a-snapshot"></a>使用快照集初始化訂閱
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  建立發行集之後，通常會建立初始快照集，並將其複製到快照集資料夾 (使用「新增發行集精靈」建立的合併式發行集預設均會發生此情況)。 然後，在訂閱的初始同步處理期間，由「散發代理程式」(針對交易式和快取式發行集) 或「合併代理程式」(針對合併式發行集) 套用至「訂閱者」。 快照集處理取決於發行集的類型：  
  
-   如果快照集用於不使用參數化篩選的快照式發行集、交易式發行集或合併式發行集，則快照集會在大量複製程式 (bcp) 檔案中包含結構描述，還會包含複寫所需的條件約束、擴充屬性、索引、觸發程序和系統資料表。 如需建立和套用快照集的詳細資訊，請參閱[建立和套用快照集](../../relational-databases/replication/create-and-apply-the-snapshot.md)。  
  
-   若快照集是專為使用參數化篩選的合併式發行集而產生，該快照集會使用兩部份處理建立而成。 首先建立結構描述快照集，其中包含複寫指令碼和已發行物件的結構描述，但不包含資料。 接下來每個訂閱皆以快照集初始化，該快照集中包含從結構描述快照集複製而來的指令碼和結構描述，以及屬於訂閱分割的資料。 如需詳細資訊，請參閱＜ [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)＞。  
  
 依照您發行集的複寫類型和發行項不同，快照集的組成檔案會不一樣。 這些檔案會複製到設定「散發者」時指定的預設快照集資料夾，或建立發行集時指定的替代快照集資料夾。  
  
|複寫類型|一般快照集檔|  
|-------------------------|---------------------------|  
|快照式複寫或異動複寫|結構描述 (.sch)、資料 (.bcp)、條件約束和索引 (.dri)、條件約束 (.idx)、觸發程序 (.trg，僅用於「訂閱者」) 以及壓縮的快照集檔案 (.cab)。|  
|合併式複寫|結構描述 (.sch)、資料 (.bcp)、條件約束和索引 (.dri)、觸發程序 (.trg)、系統資料表資料 (.sys)、衝突資料表 (.cft) 以及壓縮的快照集檔案 (.cab)。|  
  
 若快照集傳送期間中斷，會自動繼續並且不會重新傳送之前已傳送完成的檔案。 快照集代理程式的傳遞單位是每個發行集發行項的 bcp 檔案，這樣一來，只傳遞一部份的檔案就必須整個重新傳遞。 不過，繼續快照集可大幅減少資料傳輸量，且即使連接不穩定，也可以確保即時傳遞快照集。  
  
## <a name="snapshot-options"></a>快照集選項  
 使用快照集初始化訂閱時，可以使用下列選項。 您可以：  
  
-   指定代替預設快照集資料夾位置的替代快照集資料夾位置，或同時指定這兩個位置。 如需詳細資訊，請參閱＜ [Alternate Snapshot Folder Locations](../../relational-databases/replication/alternate-snapshot-folder-locations.md)＞。  
  
-   壓縮快照集以儲存在抽取式媒體，或者透過慢速網路傳送。 如需詳細資訊，請參閱＜ [Compressed Snapshots](../../relational-databases/replication/compressed-snapshots.md)＞。  
  
-   在套用快照集之前及之後執行 Transact-SQL 指令碼。 如需詳細資訊，請參閱[在套用快照集之前及之後執行指令碼](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)。  
  
-   使用檔案傳輸通訊協定 (FTP) 傳送快照集檔案。 如需詳細資訊，請參閱[透過 FTP 傳送快照集](../../relational-databases/replication/transfer-snapshots-through-ftp.md)。  
  
## <a name="see-also"></a>另請參閱  
 [初始化訂閱](../../relational-databases/replication/initialize-a-subscription.md)   
 [保護快照集資料夾](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
