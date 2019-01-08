---
title: sp_get_redirected_publisher (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_get_redirected_publisher_TSQL
- sp_get_redirected_publisher
ms.assetid: d47a9ab5-f2cc-42a8-8be9-a33895ce44f0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 22cc39e815fa5a98254f5bae3099da2745357b07
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52819310"
---
# <a name="spgetredirectedpublisher-transact-sql"></a>sp_get_redirected_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  複寫代理程式用來查詢散發者，以判斷原始發行者是否已經重新導向。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_get_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @bypass_publisher_validation = ] [0 | 1 ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@original_publisher** =] **'***original_publisher***'**  
 要發行的資料庫名稱。 *publisher_db*已**sysname**，沒有預設值。  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 要發行的資料庫名稱。 *publisher_db*已**sysname**，沒有預設值。  
  
 [ **@bypass_publisher_validation** = ] [0 | 1 ]  
 用來略過驗證重新導向的發行者。 如果為 0，則會執行驗證。 如果為 1，則不會執行驗證。 *bypass_publisher_validation*已**元**，預設值是 0。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**redirected_publisher**|**sysname**|重新導向之後的發行者名稱。|  
|**error_number**|**int**|驗證錯誤的錯誤號碼。|  
|**error_severity**|**int**|驗證錯誤的嚴重性。|  
|**error_message**|**nvarchar(4000)**|驗證錯誤訊息的文字。|  
  
## <a name="remarks"></a>備註  
 *redirected_publisher*傳回目前的發行者名稱。 如果發行者和發行資料庫沒有已重新導向使用，則傳回 null **sp_redirect_publisher**。  
  
 如果未要求驗證，或項目不存在於發行者和發行資料庫中， *error_number*並*error_severity*會傳回 0 並*error_message*會傳回 null。  
  
 如果要求驗證，則驗證預存程序[sp_validate_redirected_publisher &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)呼叫以確認重新導向的目標是發行的適當主機資料庫。 如果驗證成功， **sp_get_redirected_publisher**會傳回重新導向的發行者名稱，而 0 代表*error_number*並*error_severity*資料行和中的 null*error_message*資料行。  
  
 如果要求驗證而且失敗，則會傳回重新導向的發行者名稱以及錯誤資訊。  
  
## <a name="permissions"></a>Permissions  
 呼叫端必須是隸屬**sysadmin**固定伺服器角色**db_owner**散發資料庫或定義的發行集的發行集存取清單成員的固定的資料庫角色發行者資料庫相關聯。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
