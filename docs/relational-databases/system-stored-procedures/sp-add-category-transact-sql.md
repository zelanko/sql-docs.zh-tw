---
title: sp_add_category （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_category
- sp_add_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_category
ms.assetid: 6cca32cd-d941-4378-aed6-a7c90cb7520a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 076d5ade1f4951183578b1b46761d49dafbce8be
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "70810549"
---
# <a name="sp_add_category-transact-sql"></a>sp_add_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  將作業、警示或操作員的指定類別目錄加入伺服器中。 如需替代方法，請參閱[使用 SQL Server Management Studio 建立作業類別目錄](/sql/ssms/agent/create-a-job-category)。
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
 > [!IMPORTANT]  
 > 在[Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)上，目前不支援所有 SQL Server Agent 功能。 如需詳細資訊，請參閱[Azure SQL Database 受控執行個體與 SQL Server 的 t-sql 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。
  
## <a name="syntax"></a>語法  
  
```  
  
sp_add_category   
     [ [ @class = ] 'class', ]   
     [ [ @type = ] 'type', ]   
     { [ @name = ] 'name' }  
```  
  
## <a name="arguments"></a>引數  
`[ @class = ] 'class'`要加入之類別目錄的類別。 *class*為**Varchar （8）** ，預設值為 JOB，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|JOB|加入作業類別目錄。|  
|ALERT|加入警示類別目錄。|  
|OPERATOR|加入操作員類別目錄。|  
  
`[ @type = ] 'type'`要加入之類別目錄的類型。 *類型*為**Varchar （12）**，預設值為**LOCAL**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|LOCAL|本機作業類別目錄。|  
|多伺服器|多伺服器作業類別目錄。|  
|無|作業以外之類別的分類 **。**|  
  
`[ @name = ] 'name'`要加入之類別目錄的名稱。 在指定的類別內，這個名稱必須是唯一的。 *名稱*是**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_add_category**必須從**msdb**資料庫中執行。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行**sp_add_category**。  
  
## <a name="examples"></a>範例  
 下列範例會建立名稱為 `AdminJobs` 的本機作業類別目錄。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_category  
    @class=N'JOB',  
    @type=N'LOCAL',  
    @name=N'AdminJobs' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_delete_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [sp_help_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)   
 [sp_update_category &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [sysjobs &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)   
 [sysjobservers &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
