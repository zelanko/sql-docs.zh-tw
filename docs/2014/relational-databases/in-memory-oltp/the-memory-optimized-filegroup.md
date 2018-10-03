---
title: 記憶體最佳化檔案群組 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 14106cc9-816b-493a-bcb9-fe66a1cd4630
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: cd1a637bdf40202e5c8a973be8f4ae68f415cde8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48076559"
---
# <a name="the-memory-optimized-filegroup"></a>記憶體最佳化檔案群組
  若要建立記憶體最佳化資料表，您必須先建立記憶體最佳化檔案群組。 記憶體最佳化檔案群組會保存一個或多個容器。 每個容器都包含資料檔案及/或差異檔案。  
  
 即使 SCHEMA_ONLY 資料表中的資料列並未保存，而且記憶體最佳化資料表和原生編譯預存程序的中繼資料儲存在傳統目錄中， [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 引擎仍然需要 SCHEMA_ONLY 記憶體最佳化資料表的記憶體最佳化檔案群組，以便針對具有記憶體最佳化資料表的資料庫提供一致的體驗。  
  
 記憶體最佳化檔案群組是根據檔案資料流檔案群組，但有下列差異：  
  
-   每個資料庫只能建立一個記憶體最佳化檔案群組。 您必須明確地將檔案群組標示為包含 memory_optimized_data。 您可以在建立資料庫時建立檔案群組，或是稍後新增檔案群組：  
  
    ```  
    ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA  
    ```  
  
-   您必須將一個或多個容器加入至 MEMORY_OPTIMIZED_DATA 檔案群組。 例如：  
  
    ```  
    ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod  
    ```  
  
-   您不需要啟用檔案資料流 ([啟用及設定 FILESTREAM](../blob/enable-and-configure-filestream.md)) 也能建立記憶體最佳化檔案群組。 與檔案資料流的對應是由 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 引擎執行。  
  
-   您可以將新的容器加入至記憶體最佳化檔案群組。 您可能需要新的容器，才能擴充持久性記憶體最佳化資料表所需的儲存空間，以及在多個容器中分散 IO。  
  
-   具有記憶體最佳化檔案群組的資料移動會在 AlwaysOn 可用性群組組態中最佳化。 不同於傳送到次要複本的檔案資料流檔案，記憶體最佳化檔案群組中的檢查點檔案 (資料和差異處) 不會傳送至次要複本。 資料和差異檔案會使用次要複本上的交易記錄來建構。  
  
 以下是記憶體最佳化檔案群組的限制。  
  
-   一旦您建立記憶體最佳化檔案群組之後，就可以卸除資料庫來移除它。 在實際執行環境中，您不太可能需要移除記憶體最佳化檔案群組。  
  
-   您無法卸除非空白的容器或是將資料和差異檔案組移至記憶體最佳化檔案群組中的另一個容器。  
  
-   您無法為容器指定 MAXSIZE。  
  
## <a name="configuring-a-memory-optimized-filegroup"></a>設定記憶體最佳化檔案群組  
 您應該考慮在記憶體最佳化檔案群組中建立多個容器，並將它們分散到不同的磁碟機，以便有更多的頻寬可讓資料流入記憶體中。  
  
 當設定儲存空間時，您提供的可用磁碟空間必須是持久性記憶體最佳化資料表大小的四倍。 您也必須確定您的 IO 子系統支援您的工作負載所需的 IOPS。 如果在給定的 IOPS 上填入資料和差異檔案組，您需要 IOPS 的 3 倍來處理儲存和合併作業。 您可以將一個或多個容器加入至記憶體最佳化檔案群組，以增加儲存容量和 IOPS。  
  
 在多容器、多磁碟機的案例中，資料和差異檔案會以循環方式配置到容器中。 第一個資料檔案會從第一個容器配置，而差異檔案則是從下一個容器配置，依此方式重複這個配置模式。 如果您有奇數磁碟機 (每個都對應到一個容器)，此配置方案會在所有容器中平均分散資料檔案和差異檔案。 但是，如果您有偶數磁碟機 (每個都對應到容器)，可能會造成儲存空間不平衡，導致資料檔案對應到奇數磁碟機而差異檔案則對應到偶數磁碟機。 若要在復原時取得平衡的 IO 資料流，請考慮將資料檔案和差異檔案組放在相同的主軸/儲存體，如以下範例所示。  
  
 **範例：** 考慮記憶體最佳化檔案群組有兩個容器： 磁碟機 X 和 Y 的磁碟機上的容器 2 上的容器 1。因為資料和差異檔案的配置循環配置資源方式完成，所以容器 1 將只有資料檔案和容器 2 將只有差異檔案，這會導致不平衡的持續性儲存體，以及每秒，為資料檔案的輸入/輸出作業會明顯大於差異檔案。 將資料和差異檔案分散到磁碟機 X 和 Y 的一致的方式，建立四個容器而非兩個，並將前兩個容器對應到磁碟機 X 和 Y 的磁碟機下面兩個容器。循環配置的第一個資料和第一個差異檔案將會配置從容器 1 和容器 2 分別對應至磁碟機 X。同樣地下, 一步 的資料和差異檔案中將配置的容器 3 和容器 4 會對應到磁碟機 Y。這允許一致的方式將資料和差異檔案分散到兩個磁碟機。  
  
## <a name="see-also"></a>另請參閱  
 [建立及管理記憶體最佳化物件的儲存體](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
