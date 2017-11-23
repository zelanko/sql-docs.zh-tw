---
title: "sys.dm_exec_xml_handles (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_xml_handles
- dm_exec_xml_handles_TSQL
- sys.dm_exec_xml_handles_TSQL
- sys.dm_exec_xml_handles
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_xml_handles dynamic management function
ms.assetid: a873ce0f-6955-417a-96a1-b2ef11a83633
caps.latest.revision: "12"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c5b5b1ebf8d73a2ea3c93da337910775fcf9d43b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecxmlhandles-transact-sql"></a>sys.dm_exec_xml_handles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  傳回已開啟的使用中控制代碼的相關資訊**sp_xml_preparedocument**。  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))、 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。|  
  
## <a name="syntax"></a>語法  
  
```  
  
dm_exec_xml_handles (session_id | 0 )  
```  
  
## <a name="arguments"></a>引數  
 *session_id* | 0  
 工作階段的識別碼。 如果*session_id*指定，則此函數會傳回指定的工作階段 XML 控制代碼資訊。  
  
 如果指定 0，這個函數會傳回所有工作階段的全部 XML 控制代碼資訊。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|儲存此 XML 文件控制代碼的工作階段之工作階段識別碼。|  
|**document_id**|**int**|所傳回的 XML 文件控制代碼識別碼**sp_xml_preparedocument**。|  
|**namespace_document_id**|**int**|用於相關聯的命名空間文件已當做第三個參數，以傳遞的內部控制代碼識別碼**sp_xml_preparedocument**。 如果沒有命名空間文件，則為 NULL。|  
|**sql_handle**|**varbinary(64)**|已經定義控制代碼之 SQL 程式碼文字的控制代碼。|  
|**statement_start_offset**|**int**|目前執行的字元數的批次或預存程序的**sp_xml_preparedocument**呼叫，就會發生。 可以搭配**sql_handle**、 **statement_end_offset**，而**sys.dm_exec_sql_text**動態管理函數來擷取目前執行要求的陳述式。|  
|**statement_end_offset**|**int**|目前執行的字元數的批次或預存程序的**sp_xml_preparedocument**呼叫，就會發生。 可以搭配**sql_handle**、 **statement_start_offset**，而**sys.dm_exec_sql_text**動態管理函數來擷取目前執行要求的陳述式。|  
|**creation_time**|**datetime**|時間戳記時**sp_xml_preparedocument**呼叫。|  
|**original_document_size_bytes**|**bigint**|未剖析的 XML 文件大小 (以位元組為單位)。|  
|**original_namespace_document_size_bytes**|**bigint**|未剖析的 XML 命名空間文件大小 (以位元組為單位)。 如果沒有命名空間文件，則為 NULL。|  
|**num_openxml_calls**|**bigint**|含有此文件控制代碼的 OPENXML 呼叫數目。|  
|**row_count**|**bigint**|此文件控制代碼之所有先前的 OPENXML 呼叫傳回的資料列數目。|  
|**dormant_duration_ms**|**bigint**|自從上次呼叫 OPENXML 後經過的毫秒。 如果尚未呼叫 OPENXML，會傳回以來的毫秒數**sp_xml_preparedocument**t 呼叫。|  
  
## <a name="remarks"></a>備註  
 存留期**sql_handles**用來擷取執行呼叫的 SQL 文字**sp_xml_preparedocument**存留時間超過時間用來執行查詢的快取的計畫。 如果在快取中沒有查詢文字，就不能使用函數結果中提供的資訊來擷取資料。 如果您執行許多大型批次就有可能發生這種情況。  
  
## <a name="permissions"></a>Permissions  
 需要伺服器上的 VIEW SERVER STATE 權限，以查看呼叫端未擁有的所有工作階段或工作階段識別碼。 呼叫端永遠都可以查看自己目前工作階段識別碼的資料。  
  
## <a name="examples"></a>範例  
 下列範例選取了所有使用中的控制代碼。  
  
```  
SELECT * FROM sys.dm_exec_xml_handles(0);  
```  
  
## <a name="see-also"></a>請參閱＜  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [執行相關動態管理檢視和函數 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
