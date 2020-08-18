---
description: DROP SIGNATURE (Transact-SQL)
title: DROP SIGNATURE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP SIGNATURE
- DROP_SIGNATURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting signatures
- dropping signatures
- DROP SIGNATURE statement
- removing signatures
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 8a1fd8c5-0e75-4b2f-9d3c-c296bed56cc7
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 64a4c28705c80d68bd6f7499f059b1d0ca7f6846
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88304603"
---
# <a name="drop-signature-transact-sql"></a>DROP SIGNATURE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  從預存程序、函數、觸發程序或組件卸除數位簽章。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
  
DROP [ COUNTER ] SIGNATURE FROM module_name   
    BY <crypto_list> [ ,...n ]  
  
<crypto_list> ::=  
    CERTIFICATE cert_name  
    | ASYMMETRIC KEY Asym_key_name  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *module_name*  
 這是預存程序、函數、組件或觸發程序的名稱。  
  
 CERTIFICATE *cert_name*  
 這是預存程序、函數、組件、或觸發程序簽署所用的憑證名稱。  
  
 ASYMMETRIC KEY *Asym_key_name*  
 這是預存程序、函數、組件或觸發程序簽署所用的非對稱金鑰名稱。  
  
## <a name="remarks"></a>備註  
 您可以在 sys.crypt_properties 目錄檢視中，看到有關簽章的資訊。  
  
## <a name="permissions"></a>權限  
 需要物件的 ALTER 權限，以及憑證或非對稱金鑰的 CONTROL 權限。 如果相關聯的私密金鑰受到密碼保護，則使用者也必須有密碼。  
  
## <a name="examples"></a>範例  
 下列範例會從預存程序 `HumanResourcesDP` 移除憑證 `HumanResources.uspUpdateEmployeeLogin` 的簽章。  
  
```  
USE AdventureWorks2012;  
DROP SIGNATURE FROM HumanResources.uspUpdateEmployeeLogin   
    BY CERTIFICATE HumanResourcesDP;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.crypt_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-crypt-properties-transact-sql.md)   
 [ADD SIGNATURE &#40;Transact-SQL&#41;](../../t-sql/statements/add-signature-transact-sql.md)  
  
  
