---
title: sp_vupgrade_replication (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_vupgrade_replication_TSQL
- sp_vupgrade_replication
helpviewer_keywords:
- sp_vupgrade_replication
ms.assetid: d2c0ed66-07d1-4adc-82e5-a654376879bc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0e21e07cb9c81b65cccafda2e938057cd16f96b4
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54124408"
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
 [  **@login=**] **'**_登入_**'**  
 這是在散發資料庫中建立新的系統物件時，所用的系統管理員登入。 *login* 是預設值為 NULL 的 **sysname**。 如果這個參數不需要*security_mode*設為**1**，也就是 Windows 驗證。  
  
> [!NOTE]  
>  當您升級到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本時，會忽略這個參數。  
  
 [  **@password=**] **'**_密碼_**'**  
 這是在散發資料庫中建立新的系統物件時，所用的系統管理員密碼。 *密碼*已**sysname**，預設值是 **'** （空字串）。 如果這個參數不需要*security_mode*設為**1**，也就是 Windows 驗證。  
  
> [!NOTE]  
>  當您升級到 SQL [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本時，會忽略這個參數。  
  
 [  **@ver_old=**] **'**_old_version_**'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 這個預存程序已被取代，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未來的版本將會移除它。  
  
 [  **@force_remove=**] **'**_force_removal_**'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@security_mode=**] **'**_security_mode_**'**  
 這是在散發資料庫中建立新的系統物件時，所用的登入安全性模式。 *security_mode*已**位元**預設值是**0**。 如果**0**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]將用於驗證。 如果**1**，則會使用 Windows 驗證。  
  
> [!NOTE]  
>  當您升級到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本時，會忽略這個參數。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_vupgrade_replication**升級所有類型的複寫時，會使用。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_vupgrade_replication**。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [驗證複寫的資料](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
