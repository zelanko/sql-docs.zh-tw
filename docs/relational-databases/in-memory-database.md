---
title: 記憶體內部資料庫
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- in-memory database
- feature, in-memory database
- in-memory
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
author: briancarrig
ms.author: brcarrig
manager: amitban
ms.openlocfilehash: e4e0e6622a2a313b85dfa00df8c88044486f75f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65994996"
---
# <a name="in-memory-database"></a>記憶體內資料庫

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

記憶體內部資料庫是一種通稱，指的是利用記憶體內部式技術 SQL Server 中的功能。 隨著新記憶體內部式功能的開發，此頁面會持續更新。

## <a name="hybrid-buffer-pool"></a>混合式緩衝集區

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[混合式緩衝集區](../database-engine/configure-windows/hybrid-buffer-pool.md)可讓資料庫引擎直接存取儲存在持續性記憶體 (PMEM) 裝置上資料庫檔案中的資料頁。

## <a name="memory-optimized-tempdb-metadata"></a>記憶體最佳化 TempDB 中繼資料

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 引進[記憶體最佳化 tempdb 中繼資料](./databases/tempdb-database.md#memory-optimized-tempdb-metadata)新功能，可有效的移除某些競爭瓶頸，並解除鎖定大量 tempdb 工作負載的新層級延展性。

## <a name="in-memory-oltp"></a>記憶體內部 OLTP

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[記憶體內部 OLTP](./in-memory-oltp/in-memory-oltp-in-memory-optimization.md) 是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDS](../includes/sssds-md.md)] 中提供的頂級技術，可用來最佳化交易處理、資料擷取、資料載入及暫時性資料案例的效能。

**適用於：** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。

## <a name="persistent-memory-support-for-linux"></a>適用於 Linux 的持續性記憶體支援

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] 將持續性記憶體 (PMEM) 裝置的支援新增到 Linux，提供放置在[持續性記憶體](../linux/sql-server-linux-configure-pmem.md)上資料及交易記錄檔的完整資訊。

**適用於：** [!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] 到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。
