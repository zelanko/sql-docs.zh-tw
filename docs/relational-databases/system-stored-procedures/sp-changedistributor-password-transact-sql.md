---
title: "sp_changedistributor_password (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
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
- sp_changedistributor_password
- sp_changedistributor_password_TSQL
helpviewer_keywords:
- sp_changedistributor_password
ms.assetid: 4a496e60-414a-4026-ba7a-3e89391d39b7
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e0a9eca05a9ec182d6218149d5e800fff4f5154c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spchangedistributorpassword-transact-sql"></a>sp_changedistributor_password (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更散發者的密碼。 這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changedistributor_password [ @password= ] 'password'   
```  
  
## <a name="arguments"></a>引數  
 [  **@password=**] **'***密碼***'**  
 這是新密碼。 *密碼*是**sysname**，沒有預設值。 如果 「 散發者 」 是本機電腦，密碼**distributor_admin**變更系統登入。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changedistributor_password**用於所有複寫類型。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_changedistributor_password](../../relational-databases/replication/codesnippet/tsql/sp-changedistributor-pas_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_changedistributor_password**。  
  
## <a name="see-also"></a>請參閱＜  
 [檢視及修改複寫安全性設定](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [保護散發者](../../relational-databases/replication/security/secure-the-distributor.md)   
 [sp_adddistributor &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
