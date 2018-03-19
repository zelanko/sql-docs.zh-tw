---
title: ALTER SERVICE MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_SERVICE_MASTER_KEY_TSQL
- ALTER SERVICE MASTER KEY
dev_langs:
- TSQL
helpviewer_keywords:
- REGENERATE phrase
- FORCE option
- ALTER SERVICE MASTER KEY statement
- cryptography [SQL Server], Service Master Key
- modifying Service Master Key
- decryption [SQL Server], Service Master Key
- encryption [SQL Server], Service Master Key
- service master key [SQL Server], modifying
ms.assetid: a1e9be0e-4115-47d8-9d3a-3316d876a35e
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c4469bcbd22e0b0a74c8b891dfe3020c566a644a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="alter-service-master-key-transact-sql"></a>ALTER SERVICE MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的服務主要金鑰。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
ALTER SERVICE MASTER KEY   
    [ { <regenerate_option> | <recover_option> } ] [;]  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE  
  
<recover_option> ::=  
    { WITH OLD_ACCOUNT = 'account_name' , OLD_PASSWORD = 'password' }  
    |      
    { WITH NEW_ACCOUNT = 'account_name' , NEW_PASSWORD = 'password' }  
```  
  
## <a name="arguments"></a>引數  
 FORCE  
 指出即使有遺失資料的風險，仍應重新產生服務主要金鑰。 如需詳細資訊，請參閱本主題稍後的[變更 SQL Server 服務帳戶](#_changing)。  
  
 REGENERATE  
 指出應重新產生服務主要金鑰。  
  
 OLD_ACCOUNT **='***account_name***'**  
 指定舊的 Windows 服務帳戶名稱。  
  
> [!WARNING]  
>  這個選項已過時。 請勿使用。 請改用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員。  
  
 OLD_PASSWORD **='***password***'**  
 指定舊的 Windows 服務帳戶的密碼。  
  
> [!WARNING]  
>  這個選項已過時。 請勿使用。 請改用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員。  
  
 NEW_ACCOUNT **='***account_name***'**  
 指定新的 Windows 服務帳戶名稱。  
  
> [!WARNING]  
>  這個選項已過時。 請勿使用。 請改用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員。  
  
 NEW_PASSWORD **='***password***'**  
 指定新的 Windows 服務帳戶的密碼。  
  
> [!WARNING]  
>  這個選項已過時。 請勿使用。 請改用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員。  
  
## <a name="remarks"></a>Remarks  
 第一次需要利用服務主要金鑰來加密連結伺服器密碼、認證或資料庫主要金鑰時，會自動產生服務主要金鑰。 服務主要金鑰是以本機電腦金鑰或 Windows 資料保護 API 加密。 這個 API 會使用衍生自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶之 Windows 認證的金鑰。  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 是使用 AES 加密演算法來保護服務主要金鑰 (SMK) 及資料庫主要金鑰 (DMK)。 與早期版本中使用的 3DES 相比，AES 是一種較新的加密演算法。 將 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體升級至 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 之後，應該會重新產生 SMK 和 DMK，以將主要金鑰升級至 AES。 如需重新產生 DMK 的詳細資訊，請參閱 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)。  
  
##  <a name="_changing"></a> 變更 SQL Server 服務帳戶  
 若要變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員。 為管理服務帳戶的變更，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會儲存一個備用的服務主要金鑰，並由已將必要權限授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務群組的電腦帳戶所保護。 如果電腦經過重建，服務帳戶先前所使用的相同網域使用者可以復原服務主要金鑰。 這不適用於本機帳戶或本機系統、本機服務或網路服務帳戶。 當您要將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 移動到另一部電腦時，請使用備份和還原來移轉服務主要金鑰。  
  
 REGENERATE 片語會重新產生服務主要金鑰。 當重新產生服務主要金鑰時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會解密所有利用它加密的金鑰，然後利用新的服務主要金鑰來加密這些金鑰。 這是一項需要大量資源的作業。 除非已危害金鑰，否則，您應該將這項作業安排在低需求時進行。 如果任何一項解密失敗，整個陳述式便會失敗。  
  
 即使處理序無法擷取目前的主要金鑰，或無法解密所有利用該金鑰加密的私密金鑰，FORCE 選項仍會使金鑰重新產生處理序繼續進行。 請只有在重新產生作業失敗或無法使用 [RESTORE SERVICE MASTER KEY](../../t-sql/statements/restore-service-master-key-transact-sql.md) 陳述式來還原服務主要金鑰時，才使用 FORCE。  
  
> [!CAUTION]  
>  服務主要金鑰是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 加密階層的根。 服務主要金鑰會直接或間接保護樹狀中的所有其他金鑰和秘密。 如果在強制重新產生作業進行期間某相依金鑰無法解密，由該金鑰維護其安全的資料便會遺失。  
  
 如果您將 SQL 移至另一部電腦，則必須使用相同的服務帳戶來解密 SMK - SQL Server 將自動修正電腦帳戶加密。  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 CONTROL SERVER 權限。  
  
## <a name="examples"></a>範例  
 下列範例會重新產生服務主要金鑰。  
  
```  
ALTER SERVICE MASTER KEY REGENERATE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [RESTORE SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-service-master-key-transact-sql.md)   
 [BACKUP SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/backup-service-master-key-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
