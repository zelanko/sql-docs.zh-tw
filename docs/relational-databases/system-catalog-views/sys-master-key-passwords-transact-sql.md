---
title: 系統master_key_passwords(轉用-SQL) |微軟文件
ms.custom: ''
ms.date: 04/06/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.master_key_passwords_TSQL
- master_key_passwords_TSQL
- sys.master_key_passwords
- master_key_passwords
dev_langs:
- TSQL
helpviewer_keywords:
- sys.master_key_passwords catalog view
ms.assetid: b8e18cff-a9e6-4386-98ce-1cd855506e03
author: stevestein
ms.author: sstein
ms.openlocfilehash: 926acd9beb00102e19dbc2844e282d74bc890915
ms.sourcegitcommit: c6a2efe551e37883c1749bdd9e3c06eb54ccedc9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80752902"
---
# <a name="sysmaster_key_passwords-transact-sql"></a>sys.master_key_passwords (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  傳回**使用 sp_control_dbmasterkey_password**儲存過程添加的每個資料庫主金鑰密碼的行。 保護主要金鑰所用的密碼，是儲存在認證存放區中。 憑據名稱遵循此格式:##DBMKEY_<database_family_guid>_>_<random_password_guid>*。 密碼會儲存為認證秘密。 對於使用**sp_control_dbmasterkey_password**添加的每個密碼 **,sys.憑據**中有一行。  
  
 此檢視中的每一行都顯示**一個credential_id**和資料庫**的family_guid,** 主密鑰受與該憑據關聯的密碼保護。 **credential_id**上具有**sys.認證的**聯接將返回有用的欄位,如**create_date**和憑據名稱。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**credential_id**|**int**|密碼所屬的認證識別碼。 這個識別碼在伺服器執行個體中是唯一的。|  
|**family_guid**|**唯一識別碼**|建立時原始資料庫的唯一識別碼。 當資料庫還原或附加之後，這個 GUID 仍然不變，即使資料庫名稱改變了也是如此。<br /><br /> 如果服務主金鑰的自動解密失敗,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]則使用**family_guid**識別可能包含用於保護資料庫主密鑰的密碼的認證。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;交易-SQL&#41;的目录视图](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_control_dbmasterkey_password&#40;轉算-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [安全目錄檢視&#40;交易-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [建立對稱鍵&#40;轉算-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [加密層次結構](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
