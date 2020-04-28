---
title: sp_help_category （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_category
- sp_help_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_category
ms.assetid: 8cad1dcc-b43e-43bd-bea0-cb0055c84169
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1b44f5962e8241afa95b9e68cf75d493dff01ad5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "72304801"
---
# <a name="sp_help_category-transact-sql"></a>sp_help_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  提供指定的作業、警示或操作員的相關資訊。  
   
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_category [ [ @class = ] 'class' ]   
     [ , [ @type = ] 'type' ]   
     [ , [ @name = ] 'name' ]   
     [ , [ @suffix = ] suffix ]   
```  
  
## <a name="arguments"></a>引數  
`[ @class = ] 'class'`關於所要求資訊的類別。 *class*為**Varchar （8）**，預設值為**JOB**。 *類別*可以是下列其中一個值。  
  
|值|說明|  
|-----------|-----------------|  
|**任務**|提供作業類別目錄的相關資訊。|  
|**消息**|提供警示類別目錄的相關資訊。|  
|**操作**|提供操作員類別目錄的相關資訊。|  
  
`[ @type = ] 'type'`所要求之資訊所屬的類別目錄類型。 *type*是**Varchar （12）**，預設值是 Null，它可以是下列值之一。  
  
|值|說明|  
|-----------|-----------------|  
|**本機**|本機作業類別目錄。|  
|**MULTI -SERVER**|多伺服器作業類別目錄。|  
|**無**|**作業**以外類別的分類。|  
  
`[ @name = ] 'name'`所要求之資訊所屬的類別目錄名稱。 *name*是**sysname**，預設值是 Null。  
  
`[ @suffix = ] suffix`指定結果集中的**category_type**資料行是否為識別碼或名稱。 *尾碼*是**bit**，預設值是**0**。 **1**會將**category_type**顯示為名稱， **0**則會顯示為識別碼。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 當** \@尾碼**為**0**時， **sp_help_category**會傳回下列結果集：  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|類別目錄識別碼|  
|**category_type**|**tinyint**|類別目錄類型：<br /><br /> **1** = 本機<br /><br /> **2** = 多伺服器<br /><br /> **3** = 無|  
|**name**|**sysname**|類別目錄名稱|  
  
 當** \@尾碼**為**1**時， **sp_help_category**會傳回下列結果集：  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|類別目錄識別碼|  
|**category_type**|**sysname**|類別目錄的類型。 其中一個**本機**、**多伺服器**或**無**|  
|**name**|**sysname**|類別目錄名稱|  
  
## <a name="remarks"></a>備註  
 **sp_help_category**必須從**msdb**資料庫中執行。  
  
 如果未指定任何參數，結果集會提供所有作業類別目錄的相關資訊。  
  
## <a name="permissions"></a>權限  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-local-job-information"></a>A. 傳回本機作業資訊  
 下列範例會傳回本機環境所管理之作業的相關資訊。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_category  
    @type = N'LOCAL' ;  
GO  
```  
  
### <a name="b-returning-alert-information"></a>B. 傳回警示資訊  
 下列範例會傳回「複寫警示」類別目錄的相關資訊。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_category  
    @class = N'ALERT',  
    @name = N'Replication' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_add_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)   
 [sp_delete_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [sp_update_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
