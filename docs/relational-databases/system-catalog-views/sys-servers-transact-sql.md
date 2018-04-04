---
title: "sys.servers (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- servers_TSQL
- sys.servers_TSQL
- servers
- sys.servers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.servers catalog view
ms.assetid: 4e774ed9-4e83-4726-9f1d-8efde8f9feff
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: cc6dcb18c9961bffcf65db5f918ad54f19ca78ae
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2018
---
# <a name="sysservers-transact-sql"></a>sys.servers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  包含連結伺服器或遠端伺服器登錄，每一個資料列和本機伺服器的一個資料列**server_id** = 0。  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|連結伺服器的本機識別碼。|  
|**name**|**sysname**|當**server_id** = 0，這是伺服器名稱。<br /><br /> 當**server_id** > 0，這是連結伺服器的本機名稱。|  
|**product**|**sysname**|連結伺服器的產品名稱。 "SQL Server" 表示這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的另一個執行個體。|  
|**provider**|**sysname**|連接連結伺服器所用的 OLE DB 提供者名稱。|  
|**data_source**|**nvarchar(4000)**|OLE DB 資料來源連接屬性。|  
|**location**|**nvarchar(4000)**|OLE DB 位置連接屬性。 如果沒有，則為 NULL。|  
|**provider_string**|**nvarchar(4000)**|OLE DB 提供者字串連接屬性。<br /><br /> 除非呼叫端具有 ALTER ANY LINKED SERVER 權限，否則為 NULL。|  
|**catalog**|**sysname**|OLEDB 目錄連接屬性。 如果沒有，則為 NULL。|  
|**connect_timeout**|**int**|連接逾時 (以秒為單位)，如果沒有，則為 0。|  
|**query_timeout**|**int**|查詢逾時 (以秒為單位)，如果沒有，則為 0。|  
|**is_linked**|**bit**|0 = 已利用加入的舊式伺服器**sp_addserver**、 以不同的 RPC 和分散式交易行為。<br /><br /> 1 = 標準連結伺服器。|  
|**is_remote_login_enabled**|**bit**|已設定 RPC 選項，目的是啟用這部伺服器的內送遠端登入。|  
|**is_rpc_out_enabled**|**bit**|已啟用外寄 (從這部伺服器) RPC。|  
|**is_data_access_enabled**|**bit**|已啟用伺服器來進行分散式查詢。|  
|**is_collation_compatible**|**bit**|如果沒有其他定序資訊可用的話，便假設遠端資料的定序與本機資料相容。|  
|**uses_remote_collation**|**bit**|如果是 1，請使用遠端伺服器所報告的定序；否則，就使用下一個資料行所指定的定序。|  
|**collation_name**|**sysname**|所要使用的定序名稱，如果只使用本機，則為 NULL。|  
|**lazy_schema_validation**|**bit**|如果是 1，則查詢啟動時，不會檢查結構描述驗證。|  
|**is_system**|**bit**|這部伺服器只能被內部系統存取。|  
|**is_publisher**|**bit**|伺服器是複寫發行者。|  
|**is_subscriber**|**bit**|伺服器是複寫訂閱者。|  
|**is_distributor**|**bit**|伺服器是複寫散發者。|  
|**is_nonsql_subscriber**|**bit**|伺服器是非 SQL Server 複寫訂閱者。|  
|**is_remote_proc_transaction_promotion_enabled**|**bit**|如果是 1，呼叫遠端預存程序就會啟動分散式交易，而且會利用 MS DTC 來編列這項交易。 如需詳細資訊，請參閱 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)的資料。|  
|**modify_date**|**datetime**|上次變更伺服器資訊的日期。|  
  
## <a name="permissions"></a>Permissions  
 中的值**provider_string**一律是 NULL 除非呼叫端具有 ALTER ANY LINKED SERVER 權限。  
  
 若要檢視本機伺服器不需要權限 (**server_id** = 0)。  
  
 當您建立連結伺服器或遠端伺服器，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]建立預設登入對應，以**公用**伺服器角色。 這表示所有登入預設都可以檢視所有的連結伺服器和遠端伺服器。 若要限制這些伺服器的可見性，請移除預設登入對應執行[sp_droplinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)並指定 NULL *locallogin*參數。  
  
 如果刪除預設登入對應，則只有已明確加入成為連結登入或遠端登入的使用者可以檢視他們所擁有之登入的連結伺服器或遠端伺服器。 刪除預設登入對應之後，使用者必須具備下列權限才能檢視所有的連結伺服器和遠端伺服器：  
  
-   ALTER ANY LINKED SERVER 或 ALTER ANY LOGIN ON SERVER  
  
-   中的成員資格**setupadmin**或**sysadmin**固定伺服器角色  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [連結的伺服器目錄檢視&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)  
  
  
