---
title: 記憶體最佳化檔案群組 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 14106cc9-816b-493a-bcb9-fe66a1cd4630
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 265419b25df79ce491567cf563188ac70cdccc42
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68024961"
---
# <a name="the-memory-optimized-filegroup"></a>記憶體最佳化檔案群組
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  若要建立記憶體最佳化資料表，您必須先建立記憶體最佳化檔案群組。 記憶體最佳化檔案群組會保存一個或多個容器。 每個容器都包含資料檔案及/或差異檔案。  
  
 即使 `SCHEMA_ONLY` 資料表中的資料列並未保存，而且記憶體最佳化資料表和原生編譯預存程序的中繼資料儲存在傳統目錄中，則 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 引擎仍然需要 `SCHEMA_ONLY` 記憶體最佳化資料表的記憶體最佳化檔案群組，以便針對具有記憶體最佳化資料表的資料庫提供一致體驗。  
  
 記憶體最佳化檔案群組是根據檔案資料流檔案群組，但有下列差異：  
  
-   每個資料庫只能建立一個記憶體最佳化檔案群組。 您必須明確地將檔案群組標示為包含 memory_optimized_data。 您可以在建立資料庫時建立檔案群組，或是稍後新增檔案群組：  
  
    ```sql  
    ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA  
    ```  
  
-   您必須將一或多個容器新增至 `MEMORY_OPTIMIZED_DATA` 檔案群組。 例如：  
  
    ```sql  
    ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod  
    ```  
  
-   您不需要啟用檔案資料流 ([啟用及設定 FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)) 也能建立記憶體最佳化檔案群組。 與檔案資料流的對應是由 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 引擎執行。  
  
-   您可以將新的容器加入至記憶體最佳化檔案群組。 您可能需要新的容器，才能擴充持久性記憶體最佳化資料表所需的儲存空間，以及在多個容器中分散 IO。  
  
-   具有記憶體最佳化檔案群組的資料移動會在 AlwaysOn 可用性群組組態中最佳化。 不同於傳送到次要複本的檔案資料流檔案，記憶體最佳化檔案群組中的檢查點檔案 (資料和差異處) 不會傳送至次要複本。 資料和差異檔案會使用次要複本上的交易記錄來建構。  
  
以下是適用於記憶體最佳化檔案群組的限制：  
  
-   一旦您使用記憶體最佳化檔案群組之後，就可以透過卸除資料庫予以移除。 在實際執行環境中，您不太可能需要移除記憶體最佳化檔案群組。  
  
-   您無法卸除非空白的容器或是將資料和差異檔案組移至記憶體最佳化檔案群組中的另一個容器。    
  
## <a name="configuring-a-memory-optimized-filegroup"></a>設定記憶體最佳化檔案群組  
考慮在記憶體最佳化檔案群組中建立多個容器，並將它們分散到不同的磁碟機，以便有更多的頻寬可讓資料流入記憶體中。 
 
在多容器、多磁碟機的案例中，資料和差異檔案會以循環方式配置到容器中。 第一個資料檔案會從第一個容器配置，而差異檔案則是從下一個容器配置，依此方式重複這個配置模式。 如果您有奇數磁碟機 (每個都對應到一個容器)，此配置方案會在所有容器中平均分散資料檔案和差異檔案。 但是，如果您有偶數磁碟機 (每個都對應到容器)，可能會造成儲存空間不平衡，導致資料檔案對應到奇數磁碟機而差異檔案則對應到偶數磁碟機。 若要在復原時取得平衡的 I/O 資料流，請考慮將資料檔案和差異檔案組放在相同的主軸/儲存體。
  
當設定儲存空間時，您提供的可用磁碟空間必須是持久性記憶體最佳化資料表大小的四倍。 同時確認 I/O 子系統支援您工作負載所需的 IOPS。 如果在指定的 IOPS 上填入資料和差異檔案組，您需要 IOPS 的 3 倍來處理儲存和合併作業。 您可以將一個或多個容器加入至記憶體最佳化檔案群組，以增加儲存容量和 IOPS。  
 
> [!CAUTION]
> 若已針對記憶體最佳化檔案群組設定 `MAXSIZE` 值，且檢查點檔案超過容器的大小上限，則資料庫的狀態會變成 SUSPECT。   
> 在此情況下，請不要嘗試將資料庫設為 OFFLINE 和 ONLINE，這會造成資料庫狀態進入 RECOVERY_PENDING。
  
## <a name="see-also"></a>另請參閱  
[建立及管理記憶體最佳化物件的儲存體](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
[Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)    
[ALTER DATABASE 檔案及檔案群組選項 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) 

