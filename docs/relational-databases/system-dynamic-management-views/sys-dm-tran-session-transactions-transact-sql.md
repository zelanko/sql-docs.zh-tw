---
title: sys.databases dm_tran_session_transactions （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_tran_session_transactions
- sys.dm_tran_session_transactions
- sys.dm_tran_session_transactions_TSQL
- dm_tran_session_transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_session_transactions dynamic management view
ms.assetid: c7157491-58c2-49fe-87d7-0c9723113adf
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 61f0acde59f599394c25ec76c964b9d8b6e0c1cb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85718721"
---
# <a name="sysdm_tran_session_transactions-transact-sql"></a>sys.dm_tran_session_transactions (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asdw-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  傳回相關聯交易和工作階段的相互關聯資訊。  
  
> [!NOTE]  
>  若要從或呼叫此 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] ，請使用**dm_pdw_nodes_tran_session_transactions**的名稱。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|session_id|**int**|執行交易所在的工作階段識別碼。|  
|transaction_id|**bigint**|交易的識別碼。|  
|transaction_descriptor|**binary （8）**|與用戶端驅動程式通訊時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的交易識別碼。|  
|enlist_count|**int**|在工作階段中處理交易的作用中要求數目。|  
|is_user_transaction|**bit**|1 = 交易由使用者要求起始。<br /><br /> 0 = 系統交易。|  
|is_local|**bit**|1 = 本機交易。<br /><br /> 0 = 分散式交易或編列的已繫結工作階段交易。|  
|is_enlisted|**bit**|1 = 編列的分散式交易。<br /><br /> 0 = 非編列的分散式交易。|  
|is_bound|**bit**|1 = 交易透過繫結工作階段而作用於工作階段中。<br /><br /> 0 = 交易透過繫結工作階段而未作用於工作階段中。|  
|open_transaction_count||每個工作階段開啟中的交易數目。|  
|pdw_node_id|**int**|**適用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此散發所在節點的識別碼。|  
  
## <a name="permissions"></a>權限

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 許可權。   
在高階 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 層級上，需要 `VIEW DATABASE STATE` 資料庫的許可權。 在 [ [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 標準] 和 [基本] 層上，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。   

## <a name="remarks"></a>備註  
 透過繫結工作階段和分散式交易，交易可在一個以上的工作階段中執行。 在這些情況下，sys.dm_tran_session_transactions 將針對相同的 transaction_id 顯示多個資料列，針對執行交易所在的每一個工作階段，各顯示一個資料列。  
  
 在自動認可模式中使用 Multiple Active Result Set (MARS) 來執行多項要求，就可以使單一工作階段中有一個以上的作用中交易。 在這些情況下，sys.dm_tran_session_transactions 將針對相同的 session_id 顯示多個資料列，針對在該工作階段下執行的每一項交易，各顯示一個資料列。  
  
## <a name="see-also"></a>另請參閱  
 [動態管理 Views 和函數 &#40;Transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [交易相關的動態管理檢視和函數 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


