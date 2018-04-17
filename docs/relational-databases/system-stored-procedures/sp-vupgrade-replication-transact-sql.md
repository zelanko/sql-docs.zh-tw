---
title: sp_vupgrade_replication (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_vupgrade_replication_TSQL
- sp_vupgrade_replication
helpviewer_keywords:
- sp_vupgrade_replication
ms.assetid: d2c0ed66-07d1-4adc-82e5-a654376879bc
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d99e942d4b1aeb6e0268398800766366d3e8930f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="spvupgradereplication-transact-sql"></a>sp_vupgrade_replication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  當升級複寫伺服器時，由安裝程式啟動。 依照支援在目前產品層級進行複寫所需，來升級結構描述和系統資料。 在系統和使用者資料庫中，建立新的複寫系統物件。 這個預存程序執行於進行複寫升級的機器。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_vupgrade_replication [ [@login=] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @ver_old= ] 'old_version' ]  
    [ , [ @force_remove= ] 'force_removal' ]  
    [ , [ @security_mode= ] security_mode ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@login=**] **'***登入***'**  
 這是在散發資料庫中建立新的系統物件時，所用的系統管理員登入。 *login* 是預設值為 NULL 的 **sysname**。 如果這個參數不需要*security_mode*設**1**，也就是 Windows 驗證。  
  
> [!NOTE]  
>  當您升級到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本時，會忽略這個參數。  
  
 [  **@password=**] **'***密碼***'**  
 這是在散發資料庫中建立新的系統物件時，所用的系統管理員密碼。 *密碼*是**sysname**，預設值是**'** （空字串）。 如果這個參數不需要*security_mode*設**1**，也就是 Windows 驗證。  
  
> [!NOTE]  
>  當您升級到 SQL [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本時，會忽略這個參數。  
  
 [  **@ver_old=**] **'***old_version***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 這個預存程序已被取代，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未來的版本將會移除它。  
  
 [  **@force_remove=**] **'***force_removal***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@security_mode=**] **'***security_mode***'**  
 這是在散發資料庫中建立新的系統物件時，所用的登入安全性模式。 *security_mode*是**元**預設值是**0**。 如果**0**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]則會使用驗證。 如果**1**，則會使用 Windows 驗證。  
  
> [!NOTE]  
>  當您升級到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本時，會忽略這個參數。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_vupgrade_replication**升級所有類型的複寫時使用。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_vupgrade_replication**。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [驗證複寫的資料](../../relational-databases/replication/validate-replicated-data.md)  
  
  
