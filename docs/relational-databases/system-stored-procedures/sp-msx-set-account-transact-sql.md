---
title: sp_msx_set_account （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_msx_set_account
- sp_msx_set_account_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_set_account
ms.assetid: 314ec720-3a37-48f7-bb6b-8d5b894bf843
author: stevestein
ms.author: sstein
ms.openlocfilehash: 22372412f9c3f905b8978741b556724ca880568c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68108023"
---
# <a name="sp_msx_set_account-transact-sql"></a>sp_msx_set_account (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在目標伺服器上，設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 主要伺服器的帳戶名稱和密碼。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_msx_set_account [ @credential_name = ] 'credential_name'  | [ @credential_id = ] credential_id  
```  
  
## <a name="arguments"></a>引數  
`[ @credential_name = ] 'credential_name'`用來登入主伺服器的認證名稱。 提供的名稱必須是現有認證的名稱。 必須指定*credential_name*或*credential_id* 。  
  
`[ @credential_id = ] credential_id`用來登入主伺服器之認證的識別碼。 識別碼必須是現有認證的識別碼。 必須指定*credential_name*或*credential_id* 。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 無。  
  
## <a name="remarks"></a>備註  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會利用認證來儲存目標伺服器用來登入主要伺服器的使用者名稱和密碼資訊。 這個程序會設定這部目標伺服器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 用來登入主要伺服器的認證。  
  
 指定的認證必須是現有的認證。 如需建立認證的詳細資訊，請參閱[CREATE credential &#40;transact-sql&#41;](../../t-sql/statements/create-credential-transact-sql.md)。  
  
## <a name="permissions"></a>權限  
 **Sp_msx_set_account**的執行許可權預設為**系統管理員（sysadmin** ）固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 下列範例會將這部伺服器設定成利用 `MsxAccount` 認證來登入主要伺服器。  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sp_msx_set_account @credential_name = MsxAccount ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Agent 預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sp_msx_get_account &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-msx-get-account-transact-sql.md)  
  
  
