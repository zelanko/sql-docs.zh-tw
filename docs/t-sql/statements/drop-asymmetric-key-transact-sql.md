---
title: DROP ASYMMETRIC KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP ASYMMETRIC KEY
- DROP_ASYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], removing
- removing asymmetric keys
- encryption [SQL Server], asymmetric keys
- DROP ASYMMETRIC KEY statement
- dropping asymmetric keys
- deleting asymmetric keys
- cryptography [SQL Server], asymmetric keys
ms.assetid: bf94ac07-9b62-4318-b55b-1eed8f3a1ac6
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: fdc08d0598209e3d5fa4957ca241bfa49c60b6a2
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "67898303"
---
# <a name="drop-asymmetric-key-transact-sql"></a>DROP ASYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  從資料庫移除非對稱金鑰。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP ASYMMETRIC KEY key_name [ REMOVE PROVIDER KEY ]  
```  
  
## <a name="arguments"></a>引數  
 *key_name*  
 這是要從資料庫卸除的非對稱金鑰名稱。  
  
 REMOVE PROVIDER KEY  
 從 EKM 裝置中移除 Extensible Key Management (EKM) 金鑰。 如需可延伸金鑰管理的詳細資訊，請參閱[可延伸金鑰管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)。  
  
## <a name="remarks"></a>備註  
 無法卸除資料庫中的對稱金鑰加密所用的非對稱金鑰，或是使用者或登入所對應的非對稱金鑰。 在您卸除這類金鑰之前，必須先卸除任何對應至該金鑰的使用者或登入。 您同時也必須卸除或變更任何以非對稱金鑰加密的對稱金鑰。 您可以使用 [ALTER SYMMETRIC KEY](../../t-sql/statements/alter-symmetric-key-transact-sql.md) 的 DROP ENCRYPTION 選項，來移除非對稱金鑰進行的加密。  
  
 您可以使用 [sys.asymmetric_keys](../../relational-databases/system-catalog-views/sys-asymmetric-keys-transact-sql.md) 目錄檢視，來存取非對稱金鑰的中繼資料。 金鑰本身不能直接從資料庫內部檢視。  
  
 如果將非對稱金鑰對應到 EKM 裝置上的 Extensible Key Management (EKM) 金鑰，而且並未指定 REMOVE PROVIDER KEY 選項，則此金鑰將會從資料庫中卸除，但不會卸除此裝置。 將會發出警告。  
  
## <a name="permissions"></a>權限  
 需要非對稱金鑰的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從 `MirandaXAsymKey6` 資料庫移除非對稱金鑰 `AdventureWorks2012`。  
  
```  
USE AdventureWorks2012;  
DROP ASYMMETRIC KEY MirandaXAsymKey6;  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)  
  
  
