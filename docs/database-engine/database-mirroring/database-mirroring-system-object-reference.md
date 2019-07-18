---
title: 資料庫鏡像系統物件參考 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 6f43477ebb45812fb4e71ca501296518ed3950c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66795504"
---
# <a name="database-mirroring-system-object-reference"></a>資料庫鏡像系統物件參考
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="system-catalog-views"></a>系統目錄檢視

| 系統目錄檢視 | Description|
| :------ | :----------------------------- |
| [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   | 針對伺服器在資料庫鏡像合作關係中所扮演的每個見證角色，各包含一個資料列。 |
| &nbsp; | &nbsp; |

## <a name="system-dynamic-management-views"></a>系統動態管理檢視

| 系統動態管理檢視 | Description|
| :------ | :----------------------------- |
| [sys.dm_db_mirroring_auto_page_repair](../../relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-auto-page-repair.md)   | 針對在伺服器執行個體之任何鏡像資料庫上進行的每個自動修復頁面嘗試行為，各傳回一個資料列。  |
| [sys.dm_db_mirroring_connections](../../relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-connections.md)    | 針對為資料庫鏡像建立的每個連接，各傳回一個資料列。 |
| &nbsp; | &nbsp; |

## <a name="system-tables"></a>系統資料表

| 系統資料表 | Description|
| :------ | :----------------------------- |
| [sysdbmaintplan_databases](../../relational-databases/system-tables/sysdbmaintplan-databases-transact-sql.md)   | 傳回資料庫鏡像維護計畫的相關資訊。 |
| [sysdbmaintplan_history](../../relational-databases/system-tables/sysdbmaintplan-history-transact-sql.md)    | 傳回資料庫鏡像維護計畫記錄的相關資訊。 |
| [sysdbmaintplan_jobs](../../relational-databases/system-tables/sysdbmaintplan-jobs-transact-sql.md)    |傳回資料庫鏡像維護計畫作業的相關資訊。  |
| [sysdbmaintplans](../../relational-databases/system-tables/sysdbmaintplans-transact-sql.md)    | 傳回資料庫鏡像計畫的相關資訊。  |
| &nbsp; | &nbsp; |


## <a name="see-also"></a>另請參閱  
 [資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   

  
  
