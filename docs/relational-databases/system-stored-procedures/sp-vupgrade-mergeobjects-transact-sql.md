---
title: "sp_vupgrade_mergeobjects (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_vupgrade_mergeobjects
- sp_vupgrade_mergeobjects_TSQL
helpviewer_keywords:
- sp_vupgrade_mergeobjects
ms.assetid: 73257c2e-cc4c-48e7-9d66-7ef045bdd4f5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 83c761ec8e22321e1d46a3b9aacaf5c619c45599
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spvupgrademergeobjects-transact-sql"></a>sp_vupgrade_mergeobjects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  重新產生可用來追蹤和套用合併式複寫之資料變更的發行項特有觸發程序、預存程序和檢視。 您可以在下列情況中執行此程序：  
  
-   如果複寫所需的物件意外遭到卸除。  
  
-   如果您套用需要修改一或多個複寫物件的更新 (例如 Hotfix)。 請在套用更新之後，針對每個節點執行此程序。  
  
 執行此預存程序不需要重新初始化訂閱。 如果您將 Service Pack 或升級安裝至新版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，就不需要進行此程序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_vupgrade_mergeobjects [ [@login = ] 'login' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @security_mode = ] security_mode ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@login=**] **'***登入***'**  
 這是在散發資料庫中建立新的系統物件時，所用的系統管理員登入。 *登入*是**sysname**，預設值是 NULL。 如果這個參數不需要*security_mode*設**1**，也就是 Windows 驗證。  
  
 [  **@password=**] **'***密碼***'**  
 這是在散發資料庫中建立新的系統物件時，所用的系統管理員密碼。 *密碼*是**sysname**，預設值是**'** （空字串）。 如果這個參數不需要*security_mode*設**1**，也就是 Windows 驗證。  
  
 [  **@security_mode=**] **'***security_mode***'**  
 這是在散發資料庫中建立新的系統物件時，所用的登入安全性模式。 *security_mode*是**元**預設值是**1**。 如果**0**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]則會使用驗證。 如果**1**，則會使用 Windows 驗證。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_vupgrade_mergeobjects**僅用於合併式複寫。  
  
## <a name="permissions"></a>Permissions  
 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="see-also"></a>請參閱＜  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [升級複寫的資料庫](../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
  
