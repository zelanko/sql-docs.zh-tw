---
title: 設定記憶體最佳化資料表的儲存體 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6e005de0-3a77-4b91-b497-14cc0f9f6605
caps.latest.revision: 5
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 48cbee157bf1088ddabbf33a7a6501decd8bdefa
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393825"
---
# <a name="configuring-storage-for-memory-optimized-tables"></a>設定記憶體最佳化資料表的儲存體
  您必須設定儲存容量和每秒的輸入/輸出作業 (IOPS)。  
  
## <a name="storage-capacity"></a>儲存容量  
 請使用 [估計記憶體最佳化資料表的記憶體需求](memory-optimized-tables.md) 中的資訊來預估資料庫的持久性記憶體最佳化資料表在記憶體中的大小。 因為不會針對記憶體最佳化資料表保存索引，所以請勿包含索引的大小。 一旦您決定大小之後，您提供的磁碟空間就必須是持久性記憶體中資料表大小的四倍。  
  
## <a name="storage-performance"></a>儲存體效能  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 可能會大幅增加您的工作負載輸送量。 因此，請務必確定 IO 不是瓶頸。  
  
-   將磁碟資料表移轉到記憶體最佳化資料表時，請確定交易記錄所在的儲存媒體可以支援增加的交易記錄活動。 例如，如果您的儲存媒體支援每秒 100 MB 的交易記錄作業，而且記憶體最佳化資料表會產生五倍的效能，則交易記錄的儲存媒體也必須能夠支援五倍的效能改善，以免交易記錄活動變成效能瓶頸。  
  
-   記憶體最佳化資料表會分散在一個或多個容器的檔案中來保存。 通常每個容器都應該對應至其本身的主軸，並用於增加儲存容量及改良效能。 您必須確定儲存媒體的連續 IOPS 可以支援交易記錄輸送量的 3 倍增加量。  
  
     例如，如果記憶體最佳化資料表的交易記錄中產生 500 MB/秒的活動，記憶體最佳化資料表的儲存體必須支援 1.5 GB/秒。需要支援的 3 倍增加交易記錄輸送量來自以下的觀察： 資料和差異檔案組的初始資料時，會先寫入則需要 讀取/重新寫入為合併作業的一部分。  
  
     評估儲存體輸送量的另一個因素是記憶體最佳化資料表的復原時間。 持久性資料表中的資料必須先讀入記憶體中，然後資料庫才可以提供給應用程式使用。 一般來說，將資料載入記憶體最佳化資料表的作業可以根據 IOPS 的速度來進行。 因此，如果持久性記憶體最佳化資料表的總儲存空間為 60 GB，而您希望能夠在 1 分鐘內載入這些資料，則儲存空間的 IOPS 必須設定為每秒鐘 1 GB。  
  
-   如果您有偶數的主軸，您應該建立兩倍的容器數目，每組都對應到相同的主軸。 如果要分散 IOPS 和儲存空間，就必須這樣做。 如需詳細資訊，請參閱 <<c0> [ 記憶體最佳化檔案群組](the-memory-optimized-filegroup.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立及管理記憶體最佳化物件的儲存體](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
