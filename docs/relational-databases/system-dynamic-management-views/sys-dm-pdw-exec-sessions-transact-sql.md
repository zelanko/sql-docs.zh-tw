---
title: sys.dm_pdw_exec_sessions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31c262b3-7e4d-44c4-af71-aaef0fd1a980
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: f8d910bc9b6d85475a937940787aec7a312ef3bf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47781166"
---
# <a name="sysdmpdwexecsessions-transact-sql"></a>sys.dm_pdw_exec_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保留應用裝置上目前或最近開啟的所有工作階段的相關資訊。 它會列出每個工作階段的一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|session_id|**nvarchar(32)**|（如果工作階段結束，而且查詢正在執行的終止時間），就會執行目前的查詢或最後一項查詢的識別碼。 此檢視的索引鍵。|在系統中的所有工作階段之間是唯一的。|  
|status|**nvarchar(10)**|對於目前工作階段，識別是否在工作階段目前作用中或閒置。 對於過去的工作階段，工作階段狀態可能會顯示已關閉，或已終止 （如果已強制關閉工作階段）。|'ACTIVE'、 'CLOSED'、 'IDLE'，' 終止 '|  
|request_id|**nvarchar(32)**|在目前的查詢或執行的最後一次查詢的識別碼。|在系統中的所有要求間是唯一的。 如果沒有任何已執行，則為 null。|  
|security_id|**varbinary(85)**|執行工作階段之主體的安全性識別碼。||  
|login_name|**nvarchar(128)**|執行工作階段的主體登入名稱。|任何符合使用者的命名慣例的字串。|  
|login_time|**datetime**|日期和時間的使用者登入，並建立此工作階段。|有效**datetime**目前時間之前。|  
|query_count|**int**|擷取自建立後已執行的查詢/requeststhis 工作階段的數目。|大於或等於 0。|  
|is_transactional|**bit**|擷取工作階段是否為目前交易內與否。|自動認可為 0、 1 代表交易式。|  
|client_id|**nvarchar(255)**|擷取工作階段的用戶端資訊。|任何有效的字串。|  
|app_name|**nvarchar(255)**|擷取應用程式名稱資訊 （選擇性） 設定為在連線程序的一部分。|任何有效的字串。|  
|sql_spid|**int**|SPID id 編號。 使用`session_id`此工作階段。 使用`sql_spid`加入的資料行**sys.dm_pdw_nodes_exec_sessions**。<br /><br /> **\*\* 警告\* \*** 這個資料行包含已關閉的 Spid。||  
  
 這份檢視所保留的最大資料列的相關資訊，請參閱中的系統檢視的最大值 」 一節[最小和最大值 (SQL Server PDW)](http://msdn.microsoft.com/5243f018-2713-45e3-9b61-39b2a57401b9)主題。  
  
## <a name="permissions"></a>Permissions  
 需要 `VIEW SERVER STATE` 權限。  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
