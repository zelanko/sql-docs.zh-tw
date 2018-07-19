---
title: 設定記憶體最佳化資料表的儲存體 | Microsoft Docs
ms.custom: ''
ms.date: 10/25/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6e005de0-3a77-4b91-b497-14cc0f9f6605
caps.latest.revision: 7
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 801fa05e3bf50fbf3fdc4abf4481bc8db793ae81
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
ms.locfileid: "34327449"
---
# <a name="configuring-storage-for-memory-optimized-tables"></a>設定記憶體最佳化資料表的儲存體
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  您必須設定儲存容量和每秒的輸入/輸出作業 (IOPS)。  
  
## <a name="storage-capacity"></a>儲存容量  
 請使用 [估計記憶體最佳化資料表的記憶體需求](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md) 中的資訊來預估資料庫的持久性記憶體最佳化資料表在記憶體中的大小。 因為不會針對記憶體最佳化資料表保存索引，所以請勿包含索引的大小。 一旦您決定大小之後，您提供的磁碟空間就必須是持久性記憶體中資料表大小的四倍。  
  
## <a name="storage-iops"></a>儲存體 IOPS  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 可能會大幅增加您的工作負載輸送量。 因此，請務必確定 IO 不是瓶頸。  
  
-   將磁碟資料表移轉到記憶體最佳化資料表時，請確定交易記錄所在的儲存媒體可以支援增加的交易記錄活動。 例如，如果您的儲存媒體支援每秒 100 MB 的交易記錄作業，而且記憶體最佳化資料表會產生五倍的效能，則交易記錄的儲存媒體也必須能夠支援五倍的效能改善，以免交易記錄活動變成效能瓶頸。  
  
-   記憶體最佳化資料表會分散在一或多個容器的檢查點檔案中來保存。 通常每個容器都應該對應至其本身的存放裝置，並用於增加儲存容量及改良 IOPS。 您必須確定儲存媒體的連續 IOPS 最多可以支援 3 倍連續交易記錄輸送量。 寫入檢查點檔案若是資料檔案為 256 KB，差異檔案為 4 KB。
  
     - 例如，若記憶體最佳化資料表在交易記錄中每秒連續產生 500MB 的活動，則記憶體最佳化資料表的儲存體必須能夠每秒支援 1.5GB 的 IOPS。 支援 3 倍連續交易記錄輸送量的需求來自於以下的觀察：資料和差異檔案組會先與初始資料一起寫入，然後在合併作業中必須讀取/重新寫入。  
  
- 評估儲存體 IOPS 的另一個因素是記憶體最佳化資料表的復原時間。 持久性資料表中的資料必須先讀入記憶體中，然後資料庫才可以提供給應用程式使用。 一般來說，將資料載入記憶體最佳化資料表的作業可以根據 IOPS 的速度來進行。 因此，如果持久性記憶體最佳化資料表的總儲存空間為 60 GB，而您希望能夠在 1 分鐘內載入這些資料，則儲存空間的 IOPS 必須設定為每秒鐘 1 GB。  
  
-   如果空間允許，檢查點檔案通常會均勻分佈到所有容器。 在 SQL Server 2014 中，您必須佈建奇數的容器數目才能達到均勻分佈。從 2016 版開始，奇數和偶數的容器數目都可以達到均勻分佈。
  
## <a name="encryption"></a>加密  
 在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 中，記憶體最佳化資料表的儲存體將會在啟用資料庫上的 TDE 時加密。 如需詳細資訊，請參閱[透明資料加密 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)。 在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 中，檢查點檔案不會加密，即便在資料庫上啟用 TDE 也是一樣。
  
## <a name="see-also"></a>另請參閱  
 [建立及管理記憶體最佳化物件的儲存體](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
