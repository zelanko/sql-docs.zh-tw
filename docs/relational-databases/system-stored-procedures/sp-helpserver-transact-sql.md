---
title: sp_helpserver （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9e965a11708b2d4bbb72903a05846cb14300a5c6
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826095"
---
# <a name="sp_helpserver-transact-sql"></a>sp_helpserver (Transact-SQL)
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
`[ @server = ] 'server'`這是要報告資訊的伺服器。 若未指定*伺服器*，則會報告有關**sys.databases**中所有伺服器的資訊。 *伺服器*是**sysname**，預設值是 Null。  
  
`[ @optname = ] 'option'`這是描述伺服器的選項。 *option*是**Varchar （** 35 **）**，預設值是 Null，它必須是下列值之一。  
  
|值|說明|  
|-----------|-----------------|  
|**定序相容**|影響針對連結伺服器執行分散式查詢。 如果此選項設定為 true，|  
|**資料存取**|啟用和停用連結伺服器的分散式查詢存取。|  
|**dist**|散發者。|  
|**dpub**|這個散發者的遠端簽發者。|  
|**lazy schema validation**|在查詢開始時，略過遠端資料表的結構描述檢查。|  
|**pub**|簽發者。|  
|**4**|從指定伺服器啟用 RPC。|  
|**rpc 輸出**|啟用對指定伺服器的 RPC。|  
|**sub**|訂閱者。|  
|**系統**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**使用遠端定序**|利用遠端資料行的定序來取代本機伺服器的定序。|  
  
`[ @show_topology = ] 'show_topology'`這是指定伺服器與其他伺服器的關聯性。 *show_topology*是**Varchar （** 1 **）**，預設值是 Null。 如果*show_topology*不等於**t**或為 Null， **Sp_helpserver**會傳回 [結果集] 區段中所列的資料行。 如果*show_topology*等於**t**，除了結果集中列出的資料行之外， **sp_helpserver**也會傳回**topx**和**topy**資訊。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|伺服器名稱。|  
|**network_name**|**sysname**|伺服器的網路名稱。|  
|**status**|**Varchar （** 70 **）**|伺服器狀態。|  
|**id**|**char （** 4 **）**|伺服器的識別碼。|  
|**collation_name**|**sysname**|伺服器的定序。|  
|**connect_timeout**|**int**|連接到連結伺服器的逾時值。|  
|**query_timeout**|**int**|針對連結伺服器進行查詢的逾時值。|  
  
## <a name="remarks"></a>備註  
 一部伺服器可以有多個狀態。  
  
## <a name="permissions"></a>權限  
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
 [資料庫引擎預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_adddistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_addserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_addsubscriber &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_changesubscriber &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [sp_serveroption &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
