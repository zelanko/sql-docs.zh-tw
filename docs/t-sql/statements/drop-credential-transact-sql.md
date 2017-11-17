---
title: "卸除認證 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/19/2015
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
- DROP CREDENTIAL
- DROP_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing credentials
- DROP CREDENTIAL statement
- credentials [SQL Server], DROP CREDENTIAL statement
- authentication [SQL Server], credentials
- deleting credentials
- dropping credentials
ms.assetid: df22c826-317d-45a6-b078-186acb65f71e
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 99526bd72839ff483d39f0e78634ea27039388ae
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="drop-credential-transact-sql"></a>DROP CREDENTIAL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從伺服器中移除認證。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP CREDENTIAL credential_name  
```  
  
## <a name="arguments"></a>引數  
 *credential_name*  
 這是要從伺服器中移除之認證的名稱。  
  
## <a name="remarks"></a>備註  
 若要卸除與認證相關聯，但不卸除認證本身的密碼，請使用[ALTER CREDENTIAL](../../t-sql/statements/alter-credential-transact-sql.md)。  
  
 認證的相關資訊會顯示在**sys.credentials**目錄檢視。  
  
> [!WARNING]  
>  Proxy 會與認證相關聯。 刪除 Proxy 所使用的認證，會造成相關聯的 Proxy 不穩定。 當卸除 proxy 所使用的認證，刪除 proxy (使用[sp_delete_proxy &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)後再重新建立相關聯的 proxy 使用[sp_add_proxy &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 需要 ALTER ANY CREDENTIAL 權限。 如果是卸除系統認證，則需要 CONTROL SERVER 權限。  
  
## <a name="examples"></a>範例  
 下列範例會移除一個稱為 `Saddles` 的認證。  
  
```  
DROP CREDENTIAL Saddles;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [認證 &#40; Database engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [ALTER CREDENTIAL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  

