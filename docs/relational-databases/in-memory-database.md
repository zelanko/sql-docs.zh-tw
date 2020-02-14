---
title: 記憶體內部資料庫系統功能與技術
ms.date: 10/30/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- in-memory systems
- in-memory technologies
- in-memory features
- database, in-memory database
- system, in-memory system
- features, in-memory features
- in-memory
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
author: briancarrig
ms.author: brcarrig
manager: amitban
ms.openlocfilehash: df8bb9e603d5455a2e42393df4c40956000cb037
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "76831589"
---
# <a name="in-memory-database-systems-and-technologies"></a>記憶體內部資料庫系統與技術

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

此頁面目的是作為 SQL Server 內記憶體內部功能與技術的參考頁面。 記憶體內部資料庫系統概念是指設計來利用現代化資料庫系統上所提供較大型記憶體容量的資料庫系統。 記憶體內部資料庫在本質上可能是關聯式或非關聯式。

一般認為，記憶體內部資料庫系統效能優勢主要在於存取駐留在記憶體內的資料，其速度甚至比存取最快可用磁碟子系統上的資料還要更快 (幾個數量級)。 不過，有許多 SQL Server 工作負載能在可用記憶體中容納其整個工作集。 許多記憶體內部資料庫系統可以將資料保存於磁碟，且可能不一定能將整個資料集放在可用記憶體中。

主要用於速度較慢但耐久媒體的快速揮發性快取，是關聯式資料庫工作負載的主流。 其需要特定方法來管理工作負載。 更快的記憶體傳送速率、更大的容量甚至持續性記憶體所帶來機會都有助於開發新功能和技術，以激勵新的關聯式資料庫工作負載管理方法。

## <a name="hybrid-buffer-pool"></a>混合式緩衝集區

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[混合式緩衝集區](../database-engine/configure-windows/hybrid-buffer-pool.md)可針對具有 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的 Windows 和 Linux 平台來擴充位於位元組可定址持續性記憶體儲存裝置上資料庫檔案緩衝集區。

## <a name="memory-optimized-tempdb-metadata"></a>經記憶體最佳化的 `tempdb` 中繼資料

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 引進[記憶體最佳化 tempdb 中繼資料](./databases/tempdb-database.md#memory-optimized-tempdb-metadata)新功能，可有效的移除某些競爭瓶頸，並解除鎖定大量 tempdb 工作負載的新層級延展性。

## <a name="in-memory-oltp"></a>記憶體內部 OLTP

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[記憶體內部 OLTP](./in-memory-oltp/in-memory-oltp-in-memory-optimization.md) 是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 中提供的資料庫技術，可用來最佳化交易處理、資料擷取、資料載入及暫時性資料案例的效能。

## <a name="configuring-persistent-memory-support-for-linux"></a>設定 Linux 的持續性記憶體支援

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] 描述如何使用 `ndctl` 公用程式[持續性記憶體](../linux/sql-server-linux-configure-pmem.md)來設定持續性記憶體 (PMEM)。

## <a name="persisted-log-buffer"></a>保存的記錄緩衝區

[!INCLUDE[ssSQL16](../includes/sssql16-md.md)] 的 Service Pack 1，已針對由 WRITELOG 等候所繫結的寫入密集工作負載引進了效能最佳化。 持續性記憶體用於儲存記錄緩衝區。 此緩衝區很小 (每個使用者資料庫 20 MB)，必須排清到磁碟，才能將寫入交易記錄檔的交易強行寫入。 針對寫入密集的 OLTP 工作負載，這種排清機制可能會成為瓶頸。 使用持續性記憶體上的記錄緩衝區時，強行寫入記錄所需的作業數量會減少，從而改善整體交易時間並提升工作負載效能。 此程序稱為[記錄快取的結尾]( https://blogs.msdn.microsoft.com/bobsql/2016/11/08/how-it-works-it-just-runs-faster-non-volatile-memory-sql-server-tail-of-log-caching-on-nvdimm/)。 不過，[結尾記錄備份](./backup-restore/tail-log-backups-sql-server.md)存在衝突，傳統上的理解是，記錄結尾是已強行寫入交易記錄但尚未備份的部分。 正式的功能名稱為「保存的記錄緩衝區」，也就是此處使用的名稱。

請參閱[將保存的記錄緩衝區新增至資料庫](./databases/add-persisted-log-buffer.md)。
