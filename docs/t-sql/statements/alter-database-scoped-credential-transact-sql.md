---
description: ALTER DATABASE SCOPED CREDENTIAL (Transact-SQL)
title: ALTER DATABASE SCOPED CREDENTIAL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER DATABASE SCOPED CREDENTIAL
- ALTER_DATABASE_SCOPED_CREDENTIAL_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CREDENTIAL statement
- credentials [SQL Server], ALTER DATABASE SCOPED CREDENTIAL statement
ms.assetid: 966b75b5-ca87-4203-8bf9-95c4e00cb0b5
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 00cfd711ce130fa9c90c11000a6853082494e9bd
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124292"
---
# <a name="alter-database-scoped-credential-transact-sql"></a>ALTER DATABASE SCOPED CREDENTIAL (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  變更資料庫範圍認證的屬性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
ALTER DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *credential_name*  
 指定要變更的資料庫範圍認證的名稱。  
  
 IDENTITY **='** _identity_name_*_'_*  
 指定連接到伺服器外部時所要使用的帳戶名稱。 若要從 Azure Blob 儲存體匯入檔案，身分識別名稱必須為 `SHARED ACCESS SIGNATURE`。  如需共用存取簽章的詳細資訊，請參閱[使用共用存取簽章 (SAS)](/azure/storage/storage-dotnet-shared-access-signature-part-1)。  
    
  
 SECRET **='** _secret_*_'_*  
 指定外寄驗證所需的秘密。 從 Azure Blob 儲存體匯入檔案需要 *secret*。 針對其他用途，*secret* 可能為選擇性的。   
> [!WARNING]
>  SAS 金鑰值的開頭可能是 '?' (問號)。 當您使用 SAS 金鑰時，您必須移除前置字元 '?'。 否則您的工作可能會受阻。    
  
## <a name="remarks"></a>備註  
 當資料庫範圍認證變更時，*identity_name* 和 *secret* 的值都會重設。 如果未指定選擇性 SECRET 引數，預存秘密的值便會設為 NULL。  
  
 秘密是利用服務主要金鑰來加密的。 如果重新產生服務主要金鑰，便會利用新的服務主要金鑰來重新加密秘密。  
  
 資料庫範圍認證的相關資訊顯示在 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) 目錄檢視中。  
  
## <a name="permissions"></a>權限  
 需要認證上的 `ALTER` 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-changing-the-password-of-a-database-scoped-credential"></a>A. 變更資料庫範圍認證的密碼  
 下列範例會變更儲存在稱為 `Saddles` 之資料庫範圍認證中的祕密。 資料庫範圍認證包含 Windows 登入`RettigB` 及其密碼。 使用 SECRET 子句將新的密碼加入資料庫範圍認證中。  
  
```sql  
ALTER DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'RettigB',   
    SECRET = 'sdrlk8$40-dksli87nNN8';  
GO  
```  
  
### <a name="b-removing-the-password-from-a-credential"></a>B. 從認證移除密碼  
 下列範例會從稱為 `Frames` 的資料庫範圍認證中移除密碼。 資料庫範圍認證包含 Windows 登入 `Aboulrus8` 及密碼。 在執行陳述式之後，資料庫範圍認證的密碼為 NULL，因為未指定 SECRET 選項。  
  
```sql  
ALTER DATABASE SCOPED CREDENTIAL Frames WITH IDENTITY = 'Aboulrus8';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [認證 &#40;資料庫引擎&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
