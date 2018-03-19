---
title: DROP SYMMETRIC KEY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP SYMMETRIC KEY
- DROP_SYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], removing
- deleting symmetric keys
- encryption [SQL Server], symmetric keys
- removing symmetric keys
- dropping symmetric keys
- cryptography [SQL Server], symmetric keys
- DROP SYMMETRIC KEY statement
ms.assetid: 6150bc67-08cb-402e-9c24-b04c9654b434
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf77b14c281f4e0db0990cda321bbdf92b65f6f8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="drop-symmetric-key-transact-sql"></a>DROP SYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  從目前資料庫移除對稱金鑰。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP SYMMETRIC KEY symmetric_key_name [REMOVE PROVIDER KEY]  
```  
  
## <a name="arguments"></a>引數  
 *symmetric_key_name*  
 這是您要卸除的對稱金鑰名稱。  
  
 REMOVE PROVIDER KEY  
 從 EKM 裝置中移除 Extensible Key Management (EKM) 金鑰。 如需可延伸金鑰管理的詳細資訊，請參閱[可延伸金鑰管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)。  
  
## <a name="remarks"></a>Remarks  
 如果在目前的工作階段中開啟金鑰，陳述式會失敗。  
  
 如果將非對稱金鑰對應到 EKM 裝置上的可延伸金鑰管理 (EKM) 金鑰，而且未指定 **REMOVE PROVIDER KEY** 選項，金鑰就會從資料庫中卸除，但不會從裝置卸除，而且會發出警告。  
  
## <a name="permissions"></a>Permissions  
 需要對稱金鑰的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從目前資料庫移除名稱為 `GailSammamishKey6` 的對稱金鑰。  
  
```  
CLOSE SYMMETRIC KEY GailSammamishKey6;  
DROP SYMMETRIC KEY GailSammamishKey6;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CLOSE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-symmetric-key-transact-sql.md)   
 [可延伸金鑰管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  
