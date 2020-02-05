---
title: 加速資料庫復原 | Microsoft Docs
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- accelerated database recovery [SQL Server], recovery-only
- database recovery [SQL Server]
author: mashamsft
ms.author: mathoma
ms.reviewer: kfarlee
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8fea43ea41bc3e65fa0a6b36c7557322431e95fd
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "75245256"
---
# <a name="manage-accelerated-database-recovery"></a>管理加速資料庫復原

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

## <a name="enabling-and-controlling-adr"></a>啟用和控制 ADR

在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 中根據預設 ADR 為關閉，且可以使用 DDL 語法來控制：
```sql
ALTER DATABASE [DB] SET ACCELERATED_DATABASE_RECOVERY = {ON | OFF}
[(PERSISTENT_VERSION_STORE_FILEGROUP = { filegroup name }) ];

```

使用此語法來控制是否開啟或關閉功能，或是為「持續版本存放區」  (PVS) 資料指定特定的檔案群組。 若沒有指定檔案群組，PVS 將會儲存在 PRIMARY 檔案群組中。

## <a name="managing-the-persistent-version-store-filegroup"></a>管理持續版本存放區檔案群組
ADR 功能是以為變更建立版本，並將資料項目的不同版本儲存在 PVS 中作為基礎。
尋找 PVS 所在位置及決定如何管理 PVS 中資料的大小時，有一些考量事項。

### <a name="to-enable-adr-without-specifying-a-filegroup"></a>啟用 ADR 而不指定檔案群組

```sql
ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = ON;
GO
```

在此情況下，不會指定 PVS 檔案群組，`PRIMARY` 檔案群組會保存 PVS 資料。

### <a name="to-enable-adr-and-specify-that-the-pvs-should-be-stored-in-the-versionstorefg-filegroup"></a>啟用 ADR 並指定 PVS 應儲存在 [VersionStoreFG] 檔案群組

在執行此指令碼前，請建立檔案群組。

```sql
ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = ON
(PERSISTENT_VERSION_STORE_FILEGROUP = [VersionStoreFG])
```

### <a name="to-disable-the-adr-feature"></a>停用 ADR 功能

```sql
ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = OFF;
GO
```

即使在停用 ADR 功能後，持續版本存放區中仍然會有儲存的版本，因為系統仍需要它們來進行邏輯還原。

### <a name="change-the-location-of-the-pvs-to-a-different-filegroup"></a>將 PVS 的位置變更至不同檔案群組

您可能會因為各式各樣的理由，需要將 PVS 的位置移動到不同檔案群組。 例如，PVS 可能需要更多空間，或是更快的儲存體。

變更 PVS 位置是具有三個步驟的流程。

1. 關閉 ADR 功能。

   ```sql
   ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = OFF;
   GO
   ```

2. 等待釋放 PVS 中儲存的所有版本

   為了針對持續版本存放區，透過新的位置開啟 ADR，您必須確認所有版本資訊都已從先前的 PVS 位置清除。 若要強制進行清除，請執行命令：

   ```sql
   EXEC sys.sp_persistent_version_cleanup [database name]
   ```

   `sys.sp_persistent_version_cleanup` 預存程序是同步的，這表示它在從目前 PVS 中清除所有版本資訊前都不會完成。  一旦完成，您便可以藉由查詢 DMV `sys.dm_persistent_version_store_stats` 並檢查 `persistent_version_store_size_kb` 的值，來驗證版本資訊確實已移除。

   ```sql
   SELECT DB_Name(database_id), persistent_version_store_size_kb 
   FROM sys.dm_tran_persistent_version_store_stats where database_id = [MyDatabaseID]
   ```

   當 persistent_version_store_size_kb 的值為 0 時，您可以重新啟用 ADR 功能，設定 PVS 來使其位於新的檔案群組中。

1. 開啟 ADR 並指定 PVS 的新位置

   ```sql
   ALTER DATABASE [MyDatabase] SET ACCELERATED_DATABASE_RECOVERY = ON
   (PERSISTENT_VERSION_STORE_FILEGROUP = [VersionStoreFG])
   ```

## <a name="troubleshooting"></a>疑難排解

查詢 `sys.dm_tran_persistent_version_store_stats` 以檢查 PVS 大小。

檢查 `% of DB` 大小。 另請注意與一般大小的差異。

若 PVS 遠大於基準，或是其接近資料庫大小的 50%，該 PVS 便是大型 PVS。 

1. 根據交易識別碼，查詢 `oldest_active_transaction_id` 來擷取 `sys.dm_tran_database_transactions`，並檢查此交易是否已處在使用中狀態相當長的時間。

   使用中的交易會防止清除 PVS。

1. 若資料庫是可用性群組的一部分，請檢查 `secondary_low_water_mark`。 這與 `low_water_mark_for_ghosts` 報告的 `sys.dm_hadr_database_replica_states` 相同。 查詢 `sys.dm_hadr_database_replica_states` 來查看其中一個複本是否正在保留此值，因為這也會防止 PVS 清除。
1. 檢查 `min_transaction_timestamp` (或 `online_index_min_transaction_timestamp`，若線上 PVS 正在延誤的話)，並根據其結果，檢查資料行 `sys.dm_tran_active_snapshot_database_transactions` 的 `transaction_sequence_num` 來尋找包含正在延誤 PVS 清除舊快照集交易的工作階段。
1. 若上述項目皆不適用，這表示清除是由中止的交易延誤。 請檢查最後一次的 `aborted_version_cleaner_last_start_time` 和 `aborted_version_cleaner_last_end_time`，來查看中止的交易清除是否已完成。 `oldest_aborted_transaction_id` 應會在中止交易清除完成後向更高的方向移動。
1. 若中止交易尚未成功完成，請檢查錯誤記錄檔，尋找報告 `VersionCleaner` 問題的訊息。
