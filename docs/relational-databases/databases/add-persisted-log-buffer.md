---
title: 將保存的記錄緩衝區新增至資料庫
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- PMEM
- persistent memory
- persisted log buffer
- add log file
- create log buffer
- remove log buffer
ms.assetid: 8ead516a-1334-4f40-84b2-509d0a8ffa45
author: briancarrig
ms.author: brcarrig
manager: amitban
ms.openlocfilehash: cc455ce62708f488224c4df6245f14eef8b2053d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "76832229"
---
# <a name="add-persisted-log-buffer-to-a-database"></a>將保存的記錄緩衝區新增至資料庫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本主題描述如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]，將所保存記錄緩衝區新增至 [!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)] 中的資料庫。  
  
## <a name="permissions"></a>權限

需要資料庫的 ALTER 權限。  

## <a name="configure-persistent-memory-device-linux"></a>設定持續性記憶體裝置 (Linux)

在 [Linux](../../linux/sql-server-linux-configure-pmem.md) 中設定持續性記憶體裝置。

## <a name="configure-persistent-memory-device-windows"></a>設定持續性記憶體裝置 (Windows)

在 [Windows](/windows-server/storage/storage-spaces/deploy-pmem/) 中設定持續性記憶體裝置。
  
## <a name="add-a-persisted-log-buffer-to-a-database"></a>將保存的記錄緩衝區新增至資料庫  

下列範例會新增保存的記錄緩衝區。

```sql
ALTER DATABASE <MyDB> 
  ADD LOG FILE 
  (
    NAME = <DAXlog>, 
    FILENAME = '<Filepath to DAX Log File>', 
    SIZE = 20MB
  );
```

所放置的新記錄檔磁碟區或裝載必須使用 DAX (NTFS) 格式化，或使用 DAX 選項 (XFS/EXT4) 來裝載。

## <a name="remove-a-persisted-log-buffer"></a>移除保存的記錄緩衝區

若要安全移除保存的記錄緩衝區，資料庫必須處於單一使用者模式才能清空保存的記錄緩衝區。

下列範例會安排移除保存的記錄緩衝區。

```sql
ALTER DATABASE <MyDB> SET SINGLE_USER;
ALTER DATABASE <MyDB> REMOVE FILE <DAXlog>;
ALTER DATABASE <MyDB> SET MULTI_USER;
```

## <a name="limitations"></a>限制

[透明資料加密 (TDE)](../security/encryption/transparent-data-encryption.md) 與保存的記錄緩衝區不相容。

[可用性群組](../../t-sql/statements/create-availability-group-transact-sql.md)只能在次要複本上使用這項功能，因為其需要主要複本的一般記錄寫入語意。 不過，所有節點上都必須建立小型記錄檔 (最好是在 DAX 磁碟區或裝載上)。

## <a name="backup-and-restore-operations"></a>備份與還原作業

適用一般的還原條件。 如果保存的記錄緩衝區還原到 DAX 磁碟區或裝載，則其會繼續運作，否則可予以安全移除。
  
## <a name="next-steps"></a>後續步驟

- [How It Works (It Just Runs Faster):Non-Volatile Memory SQL Server Tail Of Log Caching on NVDIMM](https://blogs.msdn.microsoft.com/bobsql/2016/11/08/how-it-works-it-just-runs-faster-non-volatile-memory-sql-server-tail-of-log-caching-on-nvdimm/) (運作方式 (只是執行速度較快)：NVDIMM 上的非揮發性記憶體 SQL Server 結尾記錄快取)
- [Data exposed:Latency and Durability with SQL Server 2016](https://channel9.msdn.com/Shows/Data-Exposed/Latency-and-Durability-with-SQL-Server-2016) (已公開的資料：SQL Server 2016 的延遲和持久性)
- [Transaction Commit latency acceleration using Storage Class Memory in Windows Server 2016/SQL Server 2016 SP1](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/12/02/transaction-commit-latency-acceleration-using-storage-class-memory-in-windows-server-2016sql-server-2016-sp1/) (使用 Windows Server 2016/SQL Server 2016 SP1 中的儲存類別記憶體加速交易認可延遲)
