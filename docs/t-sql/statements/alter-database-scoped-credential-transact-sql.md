---
title: "ALTER DATABASE SCOPED CREDENTIAL (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER DATABASE SCOPED CREDENTIAL
- ALTER_DATABASE_SCOPED_CREDENTIAL_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CREDENTIAL statement
- credentials [SQL Server], ALTER DATABASE SCOPED CREDENTIAL statement
ms.assetid: 966b75b5-ca87-4203-8bf9-95c4e00cb0b5
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b45b0d87b846c50abc678692021c427006b3152e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="alter-database-scoped-credential-transact-sql"></a>ALTER DATABASE SCOPED CREDENTIAL (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  變更資料庫的屬性範圍認證。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
ALTER DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
```  
  
## <a name="arguments"></a>引數  
 *credential_name*  
 指定要改變資料庫範圍認證的名稱。  
  
 識別**='***identity_name***'**  
 指定連接到伺服器外部時所要使用的帳戶名稱。 若要匯入檔案，以從 Azure Blob 儲存體，身分識別名稱必須是`SHARED ACCESS SIGNATURE`。  如需有關共用的存取簽章的詳細資訊，請參閱[使用共用存取簽章 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)。  
    
  
 密碼**='***密碼***'**  
 指定外寄驗證所需的秘密。 *密碼*才可從 Azure Blob 儲存體匯入檔案。 *密碼*可能會是選擇性的其他用途。   
>  [!WARNING]
>  SAS 金鑰值可能會開始使用 '？ '（問號）。 當您使用 SAS 金鑰時，您必須移除前置字元 '？ '。 否則可能會封鎖您的工作。    
  
## <a name="remarks"></a>備註  
 當資料庫範圍認證變更，這兩者的值*identity_name*和*密碼*會重設。 如果未指定選擇性 SECRET 引數，預存秘密的值便會設為 NULL。  
  
 秘密是利用服務主要金鑰來加密的。 如果重新產生服務主要金鑰，便會利用新的服務主要金鑰來重新加密秘密。  
  
 資料庫範圍認證的相關資訊會顯示在[sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)目錄檢視。  
  
## <a name="permissions"></a>Permissions  
 需要`ALTER`權限的認證。  
  
## <a name="examples"></a>範例  
  
### <a name="a-changing-the-password-of-a-database-scoped-credential"></a>A. 變更密碼的資料庫範圍認證  
 下列範例會變更儲存在呼叫的資料庫範圍認證的密碼`Saddles`。 資料庫範圍認證包含 Windows 登入`RettigB`及其密碼。 資料庫範圍認證使用 SECRET 子句會加入新的密碼。  
  
```  
ALTER DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'RettigB',   
    SECRET = 'sdrlk8$40-dksli87nNN8';  
GO  
```  
  
### <a name="b-removing-the-password-from-a-credential"></a>B. 從認證移除密碼  
 下列範例會從名為資料庫範圍認證移除密碼`Frames`。 資料庫範圍認證包含 Windows 登入`Aboulrus8`和密碼。 陳述式之後，資料庫範圍認證將具有 NULL 密碼，因為未指定 SECRET 選項。  
  
```  
ALTER DATABASE SCOPED CREDENTIAL Frames WITH IDENTITY = 'Aboulrus8';  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [認證 &#40; Database engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [建立 DATABASE SCOPED CREDENTIAL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
