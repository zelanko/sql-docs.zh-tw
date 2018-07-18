---
title: 建立及管理記憶體最佳化物件的儲存體 | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 622aabe6-95c7-42cc-8768-ac2e679c5089
caps.latest.revision: 64
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5254d3d2c40200be5e0773d642ebed485b9cd0f0
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
ms.locfileid: "34328069"
---
# <a name="creating-and-managing-storage-for-memory-optimized-objects"></a>建立及管理記憶體最佳化物件的儲存體
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 引擎已整合到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，讓您在同一資料庫中可擁有記憶體最佳化資料表和 (傳統) 磁碟資料表。 不過，記憶體最佳化資料表的儲存體結構和磁碟資料表不同。  
  
 磁碟資料表的儲存體有下列索引鍵屬性︰  
  
-   對應至檔案群組，且檔案群組包含一或多個檔案。  
  
-   每個檔案會分成 8 頁的範圍，每頁大小為 8K 位元組。  
  
-   範圍可以跨多個資料表共用，但配置的頁面和資料表或索引之間有 1 對 1 的對應。 換句話說，一頁裡的資料列不能來自兩個或多個資料表或索引。  
  
-   資料會依需要移入記憶體 (緩衝集區)，已修改或新建的頁面則非同步寫入大部分產生隨機 IO 的磁碟。  
  
 記憶體最佳化資料表的儲存體有下列索引鍵屬性︰  
  
-   所有記憶體最佳化資料表都會對應到記憶體最佳化資料檔案群組。 這個檔案群組使用的語法和語意與 Filestream 相類似。  
  
-   沒有頁面，且資料以資料列保存。  
  
-   記憶體最佳化資料表的所有變更，都會以附加至使用中的檔案方式儲存。 讀取和寫入檔案都會循序進行。  
  
-   更新的實作方式為先插入再刪除。 刪除的資料列不會立即從儲存體移除。 刪除的資料列是根據 [記憶體最佳化資料表的持久性](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md)中所述的原則，由背景處理序 MERGE 移除。  
  
-   和磁碟資料表不同，記憶體最佳化資料表的儲存體不壓縮。 將壓縮的 (資料列或頁面) 磁碟資料表移轉至記憶體最佳化資料表時，您必須考量大小的變更。  
  
-   記憶體最佳化資料表可以是耐久的，也可以是非耐久的。 您只需要為耐久的記憶體最佳化資料表設定儲存體。  
  
 本節將描述檢查點檔案組，以及有關記憶體最佳化資料表中資料的儲存方式等其他方面。  
  
 本節主題：  
  
-   [設定記憶體最佳化資料表的儲存體](../../relational-databases/in-memory-oltp/configuring-storage-for-memory-optimized-tables.md)  
  
-   [記憶體最佳化檔案群組](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)  
  
-   [記憶體最佳化資料表的持久性](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md)  
  
-   [記憶體最佳化的資料表的檢查點作業](../../relational-databases/in-memory-oltp/checkpoint-operation-for-memory-optimized-tables.md)  
  
-   [為記憶體最佳化的物件定義持久性](../../relational-databases/in-memory-oltp/defining-durability-for-memory-optimized-objects.md)  
  
-   [比較以磁碟為基礎的資料表儲存體和記憶體最佳化資料表儲存體](../../relational-databases/in-memory-oltp/comparing-disk-based-table-storage-to-memory-optimized-table-storage.md)  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
