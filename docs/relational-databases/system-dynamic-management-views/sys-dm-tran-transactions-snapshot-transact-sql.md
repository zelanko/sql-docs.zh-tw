---
title: sys.dm_tran_transactions_snapshot (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_transactions_snapshot
- dm_tran_transactions_snapshot
- sys.dm_tran_transactions_snapshot_TSQL
- dm_tran_transactions_snapshot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_transactions_snapshot dynamic management view
ms.assetid: 03f64883-07ad-4092-8be0-31973348c647
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b91ac554186c37b2e074dd3faded49a01259222e
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262692"
---
# <a name="sysdmtrantransactionssnapshot-transact-sql"></a>sys.dm_tran_transactions_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回虛擬資料表**sequence_number**時每個快照集交易啟動。 此檢視傳回的資訊可以協助您執行下列工作：  
  
-   尋找目前作用中快照集交易的數目。  
  
-   識別特定快照集交易所忽略的資料修改。 快照集交易啟動時作用中交易進行的所有資料修改 (包括該交易認可之後所做的修改) 都會被快照集交易忽略。  
  
 例如，請考慮從下列的輸出**sys.dm_tran_transactions_snapshot**:  
  
```  
transaction_sequence_num snapshot_id snapshot_sequence_num  
------------------------ ----------- ---------------------  
59                       0           57  
59                       0           58  
60                       0           57  
60                       0           58  
60                       0           59  
60                       3           57  
60                       3           58  
60                       3           59  
60                       3           60  
```  
  
 `transaction_sequence_num` 資料行識別目前快照集交易的交易序號 (XSN)。 輸出中顯示兩個序號：`59` 和 `60`。 `snapshot_sequence_num` 資料行識別每個快照集交易啟動時作用中交易的交易序號。  
  
 輸出中顯示快照集交易 XSN-59 啟動時，有兩個作用中交易 XSN-57 和 XSN-58 正在執行。 如果 XSN-57 或 XSN-58 進行資料修改，XSN-59 會忽略這些變更，並使用資料列版本設定來維護資料庫的交易一致檢視。  
  
 快照集交易 XSN-60 會忽略 XSN-57 和 XSN-58 以及 XSN 59 所做的資料修改。  
  
## <a name="syntax"></a>語法  
  
```  
  
dm_tran_transactions_snapshot  
```  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**transaction_sequence_num**|**bigint**|快照集交易的交易序號 (XSN)。|  
|**snapshot_id**|**int**|在使用資料列版本設定之讀取認可之下啟動的每一個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的快照集識別碼。 這個值可用來產生資料庫的交易一致檢視，該資料庫支援在使用資料列版本設定之讀取認可快照集下面執行的每一項查詢。|  
|**snapshot_sequence_num**|**bigint**|當快照集交易啟動時作用中交易的交易序號。|  
  
## <a name="permissions"></a>Permissions

在  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在  [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium 層需要`VIEW DATABASE STATE`資料庫的權限。 上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]標準和基本層，則需要**伺服器系統管理員**該**Azure Active Directory 管理員**帳戶。   
  
## <a name="remarks"></a>備註  
 當快照集交易啟動時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會記錄當時作用中的所有交易。 **sys.dm_tran_transactions_snapshot**報告所有目前使用中的快照集交易的這項資訊。  
  
 每一項交易都由交易開始時指派的交易序號所識別。 交易是在 BEGIN TRANSACTION 或 BEGIN WORK 陳述式執行時啟動。 不過，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會隨著在 BEGIN TRANSACTION 或 BEGIN WORK 陳述式之後存取資料的第一個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式執行時指派交易序號。 交易序號以 1 遞增。  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [交易相關的動態管理檢視和函數 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  

