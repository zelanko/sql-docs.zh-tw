---
description: sys.dm_exec_xml_handles (Transact-SQL)
title: sys.dm_exec_xml_handles (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_xml_handles
- dm_exec_xml_handles_TSQL
- sys.dm_exec_xml_handles_TSQL
- sys.dm_exec_xml_handles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_xml_handles dynamic management function
ms.assetid: a873ce0f-6955-417a-96a1-b2ef11a83633
author: pmasl
ms.author: pelopes
monikerRange: =azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0433126f43a14aa12521c0a65cd1b4aca8441ac6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482659"
---
# <a name="sysdm_exec_xml_handles-transact-sql"></a>sys.dm_exec_xml_handles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  傳回 **sp_xml_preparedocument** 已開啟之現用控制碼的相關資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
dm_exec_xml_handles (session_id | 0 )  
```  
  
## <a name="arguments"></a>引數  
 *session_id* |0  
 工作階段的識別碼。 如果指定 *session_id* ，此函式會傳回指定之會話中 XML 控制碼的相關資訊。  
  
 如果指定 0，這個函數會傳回所有工作階段的全部 XML 控制代碼資訊。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|儲存此 XML 文件控制代碼的工作階段之工作階段識別碼。|  
|**document_id**|**int**|**Sp_xml_preparedocument** 所傳回的 XML 檔案控制代碼識別碼。|  
|**namespace_document_id**|**int**|用於相關聯命名空間檔的內部控制碼識別碼，已做為第三個參數傳遞至 **sp_xml_preparedocument**。 如果沒有命名空間文件，則為 NULL。|  
|**sql_handle**|**varbinary(64)**|已經定義控制代碼之 SQL 程式碼文字的控制代碼。|  
|**statement_start_offset**|**int**|目前執行的批次或預存程式中的字元數， **sp_xml_preparedocument** 呼叫會在此執行。 可以與 **sql_handle**、 **statement_end_offset** 和 **sys.dm_exec_sql_text** 動態管理函數一起使用，以取得要求的目前執行中語句。|  
|**statement_end_offset**|**int**|目前執行的批次或預存程式中的字元數， **sp_xml_preparedocument** 呼叫會在此執行。 可以與 **sql_handle**、 **statement_start_offset** 和 **sys.dm_exec_sql_text** 動態管理函數一起使用，以取得要求的目前執行中語句。|  
|**creation_time**|**datetime**|呼叫 **sp_xml_preparedocument** 時的時間戳記。|  
|**original_document_size_bytes**|**bigint**|未剖析的 XML 文件大小 (以位元組為單位)。|  
|**original_namespace_document_size_bytes**|**bigint**|未剖析的 XML 命名空間文件大小 (以位元組為單位)。 如果沒有命名空間文件，則為 NULL。|  
|**num_openxml_calls**|**bigint**|含有此文件控制代碼的 OPENXML 呼叫數目。|  
|**row_count**|**bigint**|此文件控制代碼之所有先前的 OPENXML 呼叫傳回的資料列數目。|  
|**dormant_duration_ms**|**bigint**|自從上次呼叫 OPENXML 後經過的毫秒。 如果尚未呼叫 OPENXML，則會傳回 **sp_xml_preparedocumen** t 呼叫之後的毫秒數。|  
  
## <a name="remarks"></a>備註  
 **Sql_handles** 的存留期，用來取出執行呼叫的 sql 文字 **sp_xml_preparedocument** 存留時間超過用來執行查詢的快取計畫。 如果在快取中沒有查詢文字，就不能使用函數結果中提供的資訊來擷取資料。 如果您執行許多大型批次就有可能發生這種情況。  
  
## <a name="permissions"></a>權限  
 需要伺服器上的 VIEW SERVER STATE 權限，以查看呼叫端未擁有的所有工作階段或工作階段識別碼。 呼叫端永遠都可以查看自己目前工作階段識別碼的資料。      
  
## <a name="examples"></a>範例  
 下列範例選取了所有使用中的控制代碼。  
  
```  
SELECT * FROM sys.dm_exec_xml_handles(0);  
```  
  
## <a name="see-also"></a>另請參閱  
 <br>[動態管理檢視和函數 (Transact-sql) ](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
 <br>[執行相關的動態管理檢視和函數 (Transact-sql) ](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)
 <br>[sp_xml_preparedocument (Transact-sql) ](../system-stored-procedures/sp-xml-preparedocument-transact-sql.md)
 <br>[sp_xml_removedocument (Transact-SQL)](../system-stored-procedures/sp-xml-removedocument-transact-sql.md)


 
  
  
