---
title: "ALTER ASYMMETRIC KEY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 04/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_ASYMMETRIC_KEY_TSQL
- ALTER ASYMMETRIC KEY
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTION BY PASSWORD option
- passwords [SQL Server], asymmetric keys
- encryption [SQL Server], asymmetric keys
- DECRYPTION BY PASSWORD option
- ALTER ASYMMETRIC KEY statement
- asymmetric keys [SQL Server], modifying
ms.assetid: 958e95d6-fbe6-43e8-abbd-ccedbac2dbac
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 81ae1caa65cac678ecd1ddeef0326d68e291ba36
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="alter-asymmetric-key-transact-sql"></a>ALTER ASYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  變更非對稱金鑰的屬性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
ALTER ASYMMETRIC KEY Asym_Key_Name <alter_option>  
  
<alter_option> ::=  
      <password_change_option>   
    | REMOVE PRIVATE KEY   

<password_change_option> ::=  
    WITH PRIVATE KEY ( <password_option> [ , <password_option> ] )  

<password_option> ::=  
      ENCRYPTION BY PASSWORD = 'strongPassword'  
    | DECRYPTION BY PASSWORD = 'oldPassword'  
```  
  
## <a name="arguments"></a>引數  
 *Asym_Key_Name*  
 這是非對稱金鑰在資料庫中的識別名稱。  
  
 REMOVE PRIVATE KEY  
 從非對稱金鑰移除私密金鑰。不移除公開金鑰。  
  
 WITH PRIVATE KEY  
 變更私密金鑰的保護。  
  
 ENCRYPTION BY PASSWORD **='***stongPassword***'**  
 指定用來保護私密金鑰的新密碼。 *密碼*必須符合正在執行的執行個體之電腦的 Windows 密碼原則需求[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果省略這個選項，則由資料庫主要金鑰加密此私密金鑰。  
  
 DECRYPTION BY PASSWORD **='***oldPassword***'**  
 指定目前用來保護私密金鑰的舊密碼。 如果是利用資料庫主要金鑰加密私密金鑰，則不需要這個選項。  
  
## <a name="remarks"></a>備註  
 如果沒有資料庫主要金鑰，則需要 ENCRYPTION BY PASSWORD 選項，而且如果沒有提供密碼，作業會失敗。 如需如何建立資料庫主要金鑰的相關資訊，請參閱[CREATE MASTER KEY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-master-key-transact-sql.md).  
  
 您可以利用 ALTER ASYMMETRIC KEY 指定 PRIVATE KEY 選項 (如下表所示) 來變更私密金鑰的保護。  
  
|變更保護|ENCRYPTION BY PASSWORD|DECRYPTION BY PASSWORD|  
|----------------------------|----------------------------|----------------------------|  
|從舊密碼到新密碼|必要項|Required|  
|從密碼到主要金鑰|省略|Required|  
|從主要金鑰到密碼|Required|省略|  
  
 必須先開啟資料庫主要金鑰，才可以利用它來保護私密金鑰。 如需詳細資訊，請參閱[OPEN MASTER KEY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/open-master-key-transact-sql.md).  
  
 若要變更非對稱金鑰的擁有權，請使用[ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 若要移除私密金鑰，則需要非對稱金鑰的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-changing-the-password-of-the-private-key"></a>A. 變更私密金鑰的密碼  
 下列範例會變更用來保護非對稱金鑰 `PacificSales09` 之私密金鑰的密碼。 新密碼會是 `<enterStrongPasswordHere>`。  
  
```  
ALTER ASYMMETRIC KEY PacificSales09   
    WITH PRIVATE KEY (  
    DECRYPTION BY PASSWORD = '<oldPassword>',  
    ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>');  
GO  
```  
  
### <a name="b-removing-the-private-key-from-an-asymmetric-key"></a>B. 從非對稱金鑰移除私密金鑰  
 下列範例會從 `PacificSales19` 移除私密金鑰，只留下公開金鑰。  
  
```  
ALTER ASYMMETRIC KEY PacificSales19 REMOVE PRIVATE KEY;  
GO  
```  
  
### <a name="c-removing-password-protection-from-a-private-key"></a>C. 移除私密金鑰的密碼保護  
 下列範例會從私密金鑰移除密碼保護，並利用資料庫主要金鑰保護私密金鑰。  
  
```  
OPEN MASTER KEY;  
ALTER ASYMMETRIC KEY PacificSales09 WITH PRIVATE KEY (  
    DECRYPTION BY PASSWORD = '<enterStrongPasswordHere>' );  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [SQL Server 和資料庫加密金鑰 &#40;Database Engine&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [開啟主要金鑰 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [可延伸金鑰管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  

