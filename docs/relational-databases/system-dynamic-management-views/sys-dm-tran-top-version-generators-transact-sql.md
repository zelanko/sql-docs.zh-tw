---
title: sys.dm_tran_top_version_generators (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_tran_top_version_generators
- sys.dm_tran_top_version_generators
- dm_tran_top_version_generators_TSQL
- sys.dm_tran_top_version_generators_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_top_version_generators dynamic management view
ms.assetid: cec7809b-ba8a-4df9-b5bb-d4f651ff1a86
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 300a9dcc5a73875f955bc295785db631b873a99d
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43110865"
---
# <a name="sysdmtrantopversiongenerators-transact-sql"></a>sys.dm_tran_top_version_generators (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對產生版本存放區中大部分版本的物件，傳回一份虛擬資料表。 **sys.dm_tran_top_version_generators**傳回的前 256 彙總記錄長度會依**database_id**並**rowset_id**。 **sys.dm_tran_top_version_generators**擷取資料，藉由查詢**dm_tran_version_store**虛擬資料表。 **sys.dm_tran_top_version_generators**是效率不佳的檢視，以執行，因為此檢視會查詢版本存放區，以及版本存放區可能非常龐大。 建議您使用這個函數，尋找版本存放區的最大取用者。  
  
> [!NOTE]  
>  若要呼叫這個屬性從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或是[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_tran_top_version_generators**。  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.dm_tran_top_version_generators  
```  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|資料庫識別碼。|  
|**rowset_id**|**bigint**|資料列集識別碼。|  
|**aggregated_record_length_in_bytes**|**int**|每個記錄長度總和**database_id**並**rowset_id 配對**版本存放區中。|  
|**pdw_node_id**|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 這個分佈是在節點的識別碼。|  
  
## <a name="permissions"></a>Permissions

在  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在  [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   

## <a name="remarks"></a>備註  
 因為**sys.dm_tran_top_version_generators**可能必須讀取許多頁面，因為它會掃描整個版本存放區中，執行**sys.dm_tran_top_version_generators**可能會干擾系統效能。  
  
## <a name="examples"></a>範例  
 下列範例使用的測試案例中有四筆並行交易正在 ALLOW_SNAPSHOT_ISOLATION 和 READ_COMMITTED_SNAPSHOT 選項都設為 ON 的資料庫中執行，而每一筆交易都由一個交易序號 (XSN) 識別。 正在執行的交易包括：  
  
-   XSN-57 是在可序列化隔離下執行的更新作業。  
  
-   XSN-58 與 XSN-57 相同。  
  
-   XSN-59 是在快照集隔離下執行的選取作業。  
  
-   XSN-60 與 XSN-59 相同。  
  
 執行以下查詢：  
  
```  
SELECT  
    database_id,  
    rowset_id,  
    aggregated_record_length_in_bytes  
  FROM sys.dm_tran_top_version_generators;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
database_id rowset_id            aggregated_record_length_in_bytes  
----------- -------------------- ---------------------------------  
9           72057594038321152    87  
9           72057594038386688    33  
```  
  
 輸出會顯示所建立的所有版本`database_id``9`和兩個資料表產生的版本。  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [交易相關的動態管理檢視和函數 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


