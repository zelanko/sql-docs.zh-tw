---
title: sys.databases dm_tran_commit_table （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_tran_commit_table
- dm_tran_commit_table_TSQL
- sys.dm_tran_commit_table
- sys.dm_tran_commit_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_commit_table dynamic management view
ms.assetid: 732d23c5-1f6c-4e96-bc85-8f29b520cf0e
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4bd5b497f1d96f813570282f785fe0cbfe73265d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68017934"
---
# <a name="change-tracking---sysdm_tran_commit_table"></a>變更追蹤-sys. dm_tran_commit_table
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 變更追蹤所追蹤之資料表所認可的每個交易，各顯示一個資料列。 為了可支援性而提供的 sys.dm_tran_commit_table 管理檢視會公開交易相關的資訊，變更追蹤會將該資訊儲存在 sys.syscommittab 系統資料表內。 sys.syscommittab 資料表會提供從資料庫特有交易識別碼到交易的認可記錄序號 (LSN) 和認可時間戳記之間的有效率、持續性對應。 儲存在 sys.syscommittab 資料表中而且由這個管理檢視所公開的資料會根據設定變更追蹤時指定的保留週期進行清除。  
  
> [!NOTE]  
>  若要從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]呼叫此，請使用**dm_pdw_nodes_tran_commit_table**的名稱。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|commit_ts|**Bigint**|單純遞增數字，當做每一筆認可之交易的資料庫特有時間戳記。|  
|xdes_id|**Bigint**|交易之資料庫特有的內部識別碼。|  
|commit_lbn|**Bigint**|包含交易之認可記錄檔記錄的記錄區塊數目。|  
|commit_csn|**Bigint**|交易之執行個體特有的認可序號。|  
|commit_time|**smalldatetime**|認可交易的時間。|  
|pdw_node_id|**int**|**適用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此散發所在節點的識別碼。|  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [關於變更追蹤 &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)  
  
  


