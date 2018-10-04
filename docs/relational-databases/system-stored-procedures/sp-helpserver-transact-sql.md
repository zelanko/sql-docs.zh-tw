---
title: sp_helpserver (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpserver
- sp_helpserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpserver
ms.assetid: e8f42de7-c738-41c3-8bf5-dbd559dc7184
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a543aa923d892e12bc3baea0e3aa9d1f9c3e7504
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47827676"
---
# <a name="sphelpserver-transact-sql"></a>sp_helpserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  報告有關特定遠端或複寫伺服器的資訊，或這兩種類型之所有伺服器的相關資訊。 提供伺服器名稱、伺服器的網路名稱、伺服器的複寫狀態、伺服器的識別碼，以及定序名稱。 另外，也提供連接到連結伺服器或查詢連結伺服器的逾時值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpserver [ [ @server = ] 'server' ]   
  [ , [ @optname = ] 'option' ]   
  [ , [ @show_topology = ] 'show_topology' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@server =** ] **'***server***'**  
 這是報告之資訊的相關伺服器。 當*伺服器*未指定中的所有伺服器都在報導**master.sys.servers**。 *伺服器*已**sysname**，預設值是 NULL。  
  
 [  **@optname =** ] **'***選項***'**  
 這是描述伺服器的選項。 *選項*已**varchar (** 35 **)**，預設值是 NULL，而且必須是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**定序相容**|影響針對連結伺服器執行分散式查詢。 如果此選項設定為 true，|  
|**資料存取**|啟用和停用連結伺服器的分散式查詢存取。|  
|**dist**|散發者。|  
|**dpub**|這個散發者的遠端簽發者。|  
|**延遲結構描述驗證**|在查詢開始時，略過遠端資料表的結構描述檢查。|  
|**pub**|簽發者。|  
|**rpc**|從指定伺服器啟用 RPC。|  
|**rpc 輸出**|啟用對指定伺服器的 RPC。|  
|**sub**|訂閱者。|  
|**system**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**使用遠端定序**|利用遠端資料行的定序來取代本機伺服器的定序。|  
  
 [  **@show_topology =** ] **'***show_topology***'**  
 這是指定伺服器與其他伺服器的關聯性。 *show_topology*已**varchar (** 1 **)**，預設值是 NULL。 如果*show_topology*不等於**t**是 NULL，或**sp_helpserver**傳回結果集一節中列出的資料行。 如果*show_topology*等於**t**，列出結果集中的資料行除了**sp_helpserver**也會傳回**topx**和**topy**資訊。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|伺服器名稱。|  
|**network_name**|**sysname**|伺服器的網路名稱。|  
|**status**|**varchar (** 70 **)**|伺服器狀態。|  
|**id**|**char (** 4 **)**|伺服器的識別碼。|  
|**collation_name**|**sysname**|伺服器的定序。|  
|**connect_timeout**|**int**|連接到連結伺服器的逾時值。|  
|**query_timeout**|**int**|針對連結伺服器進行查詢的逾時值。|  
  
## <a name="remarks"></a>備註  
 一部伺服器可以有多個狀態。  
  
## <a name="permissions"></a>Permissions  
 不檢查任何權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-displaying-information-about-all-servers"></a>A. 顯示所有伺服器的相關資訊  
 下列範例會利用未設定任何參數的 `sp_helpserver` 來顯示所有伺服器的相關資訊。  
  
```  
USE master;  
GO  
EXEC sp_helpserver;  
```  
  
### <a name="b-displaying-information-about-a-specific-server"></a>B. 顯示特定伺服器的相關資訊  
 下列範例會顯示 `SEATTLE2` 伺服器的所有相關資訊。  
  
```  
USE master;  
GO  
EXEC sp_helpserver 'SEATTLE2';  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_adddistpublisher &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_addserver &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_addsubscriber &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_changesubscriber &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropserver &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [sp_dropsubscriber &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpremotelogin &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
