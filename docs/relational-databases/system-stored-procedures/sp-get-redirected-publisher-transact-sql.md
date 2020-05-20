---
title: sp_get_redirected_publisher （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 55a0c2509a52bb77a4f8ea9779210dac27bc86db
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820417"
---
# <a name="sp_get_redirected_publisher-transact-sql"></a>sp_get_redirected_publisher (Transact-SQL)
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
`[ @original_publisher = ] 'original_publisher'`原先發行資料庫之 SQL Server 實例的名稱。 *original_publisher*是**sysname**，沒有預設值。
  
`[ @publisher_db = ] 'publisher_db'`要發行之資料庫的名稱。 *publisher_db*是**sysname**，沒有預設值。  
  
`[ @bypass_publisher_validation = ] [0 | 1 ]`用來略過重新導向發行者的驗證。 如果是0，則會執行驗證。 如果為 1，則不會執行驗證。 *bypass_publisher_validation*是**bit**，預設值是0。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**redirected_publisher**|**sysname**|重新導向之後的發行者名稱。|  
|**error_number**|**int**|驗證錯誤的錯誤號碼。|  
|**error_severity**|**int**|驗證錯誤的嚴重性。|  
|**error_message**|**nvarchar(4000)**|驗證錯誤訊息的文字。|  
  
## <a name="remarks"></a>備註  
 *redirected_publisher*會傳回目前的發行者名稱。 如果尚未使用**sp_redirect_publisher**重新導向發行者和發行資料庫，則會傳回 null。  
  
 如果未要求驗證，或是發行者和發行資料庫沒有專案存在， *error_number*和*error_severity*就會傳回0，而*error_message*會傳回 null。  
  
 如果要求驗證，則會呼叫驗證預存[程式 sp_validate_redirected_publisher &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md) ，以驗證重新導向的目標是否為發行資料庫的合適主控制項。 如果驗證成功， **sp_get_redirected_publisher**會傳回重新導向的發行者名稱、0（代表*error_number* ）和*error_severity*資料行，以及*error_message*資料行中的 null。  
  
 如果要求驗證而且失敗，則會傳回重新導向的發行者名稱以及錯誤資訊。  
  
## <a name="permissions"></a>權限  
 呼叫者必須是**系統管理員（sysadmin** ）固定伺服器角色的成員、散發資料庫的**db_owner**固定資料庫角色，或是與發行者資料庫相關聯之定義發行集的發行集存取清單的成員。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的複寫預存程式](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
