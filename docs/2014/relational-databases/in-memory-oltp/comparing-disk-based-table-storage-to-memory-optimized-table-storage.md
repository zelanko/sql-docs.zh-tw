---
title: 比較以磁碟為基礎的資料表儲存體和記憶體最佳化資料表儲存體 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: eacf443c-001a-445f-ad1c-5f5a45eca6f4
caps.latest.revision: 4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 88cc69ce411873e78c5ede030a61e59850289653
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394617"
---
# <a name="comparing-disk-based-table-storage-to-memory-optimized-table-storage"></a>比較以磁碟為基礎的資料表儲存體和記憶體最佳化資料表儲存體
  
  
|類別|以磁碟為基礎的資料表|持久性記憶體最佳化的資料表|  
|----------------|-----------------------|-------------------------------------|  
|DDL|中繼資料資訊會儲存在資料庫的主要檔案群組中的系統資料表內，而且可透過目錄檢視加以存取。|中繼資料資訊會儲存在資料庫的主要檔案群組中的系統資料表內，而且可透過目錄檢視加以存取。|  
|結構|資料列會儲存在 8 千個頁面中。 頁面只會儲存來自相同資料表的資料列。|資料列會儲存為個別的資料列。 沒有頁面結構。 資料檔案中的兩個連續資料列可屬於不同的記憶體最佳化的資料表。|  
|索引|索引會儲存在類似於資料列的頁面結構中。|只有索引定義會保存下來 (非索引資料列)。 索引會在記憶體中維護，而且當記憶體最佳化的資料表在重新啟動資料庫的過程中載入記憶體中時，將會重新產生索引。 因為索引資料列不會保存下來，所以索引變更不會進行任何記錄。|  
|DML 作業|第一步是尋找頁面，然後將它載入緩衝集區內。<br /><br /> Insert<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在頁面上插入資料列，以代表資料列排序。<br /><br /> DELETE<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在頁面上找出要刪除的資料列，並將它標記為刪除。<br /><br /> Update<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在頁面上找出資料列。 非索引鍵資料行會就地完成更新。 索引鍵資料行的更新是由刪除和插入作業所完成。<br /><br /> 當 DML 作業完成後，受影響的頁面會排清到磁碟，這是最小記錄作業的緩衝集區原則、檢查點或交易認可的一部分。 頁面上的讀寫作業都會產生不必要的 I/O。|如果是記憶體最佳化的資料表，因為資料常駐於記憶體中，所以 DML 作業會直接在記憶體中完成。 有背景執行緒會讀取記憶體最佳化之資料表的記錄檔記錄，並將其保存在資料和差異檔案中。 更新會產生新的資料列版本。 但是更新會記錄為插入之後的刪除。|  
|分割區|資料操作會分割資料，導致磁碟上不連續的部分填滿頁面和邏輯連續頁面。 這樣會降低資料存取效能，而且會要求您重組資料。|記憶體最佳化的資料不會儲存在頁面上，所以不會分割資料。 不過，因為資料列已更新和刪除，所以必須壓縮資料和差異檔案。 這是由根據合併原則的背景 MERGE 執行緒所完成。|  
  
## <a name="see-also"></a>另請參閱  
 [建立及管理記憶體最佳化物件的儲存體](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
