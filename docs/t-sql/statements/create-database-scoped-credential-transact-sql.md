---
title: "建立 DATABASE SCOPED CREDENTIAL (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATABASE SCOPED CREDENTIAL
- DATABASE_SCOPED_CREDENTIAL_TSQL
- SCOPED_TSQL
- CREATE_DATABASE_SCOPED_CREDENTIAL
- CREATE_DATABASE_SCOPED_CREDENTIAL_TSQL
- SCOPED_CREDENTIAL_TSQL
- SCOPED_CREDENTIAL
helpviewer_keywords:
- DATABASE SCOPED CREDENTIAL statement
- credentials [SQL Server], DATABASE SCOPED CREDENTIAL statement
ms.assetid: fe830577-11ca-44e5-953b-2d589d54d045
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: 49ff2aa300fc8f8e74424ae6e334bee823e8176c
ms.contentlocale: zh-tw
ms.lasthandoff: 10/06/2017

---
# <a name="create-database-scoped-credential-transact-sql"></a>建立 DATABASE SCOPED CREDENTIAL (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  建立資料庫的認證。 資料庫認證未對應至伺服器登入或資料庫使用者。 認證可由資料庫來存取外部的位置，每當資料庫正在執行需要存取的作業。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
 
CREATE DATABASE SCOPED CREDENTIAL credential_name   
WITH IDENTITY = 'identity_name'  
    [ , SECRET = 'secret' ]  
  
```  
  
## <a name="arguments"></a>引數  
 *credential_name*  
 指定所要建立資料庫範圍認證的名稱。 *credential_name*不能以數字 （#） 符號開頭。 系統認證必須以 ## 為開頭。  
  
 識別**='***identity_name***'**  
 指定連接到伺服器外部時所要使用的帳戶名稱。 若要匯入檔案，以從 Azure Blob 儲存體，身分識別名稱必須是`SHARED ACCESS SIGNATURE`。  如需有關共用的存取簽章的詳細資訊，請參閱[使用共用存取簽章 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)。  
  
 密碼**='***密碼***'**  
 指定外寄驗證所需的秘密。 `SECRET`需要從 Azure Blob 儲存體匯入檔案。   
>  [!WARNING]
>  SAS 金鑰值可能會開始使用 '？ '（問號）。 當您使用 SAS 金鑰時，您必須移除前置字元 '？ '。 否則可能會封鎖您的工作。  
  
## <a name="remarks"></a>備註  
 資料庫範圍認證是包含才能連接至外部資源的驗證資訊的記錄[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 大部分認證都包含 Windows 使用者和密碼。  
  
 建立資料庫範圍認證之前，資料庫必須有主要金鑰來保護認證。 如需詳細資訊，請參閱 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)。  
  
 當 IDENTITY 是 Windows 使用者時，秘密可以是密碼。 秘密是利用服務主要金鑰來加密的。 如果重新產生服務主要金鑰，便會利用新的服務主要金鑰來重新加密秘密。  
   
 資料庫範圍認證的相關資訊會顯示在[sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)目錄檢視。  
  
 
 Hereare 資料庫的某些應用程式範圍的認證：  
  
- [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]您可以使用資料庫範圍認證來存取非公用 Azure blob 儲存體或含有 PolyBase 的 Kerberos 保護的 Hadoop 叢集。 若要進一步了解，請參閱[CREATE EXTERNAL DATA SOURCE (TRANSACT-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)。  

- [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]PolyBase 會使用資料庫範圍認證以存取非公用 Azure blob 儲存體。 若要進一步了解，請參閱[CREATE EXTERNAL DATA SOURCE (TRANSACT-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)。
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]使用資料庫範圍的認證的全域查詢功能。 這是資料庫的多個分區進行查詢的能力。  
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]要寫入 Azure blob 儲存體擴充的事件檔案，會使用資料庫範圍認證。  
  
- [!INCLUDE[ssSDS](../../includes/sssds-md.md)]使用資料庫範圍的認證的彈性集區。 如需詳細資訊，請參閱[有效駕馭爆炸性成長的彈性資料庫](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)  

- [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)和[OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)使用資料庫範圍的認證來存取 Azure blob 儲存體的資料。 如需詳細資訊，請參閱[範例的大量資料的存取 Azure Blob 儲存體](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)。 
  
## <a name="permissions"></a>Permissions  
 需要**控制項**資料庫的權限。  
  
## <a name="examples"></a>範例  
### <a name="a-creating-a-database-scoped-credential-for-your-application"></a>A. 建立資料庫範圍認證您的應用程式。
 下列範例會建立資料庫範圍認證呼叫`AppCred`。 資料庫範圍認證包含 Windows 使用者`Mary5`和密碼。  
  
```tsql  
-- Create a db master key if one does not already exist, using your own password.  
CREATE MASTER KEY ENCRYPTION BY PASSWORD='<EnterStrongPasswordHere>';  
  
-- Create a database scoped credential.  
CREATE DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'Mary5',   
    SECRET = '<EnterStrongPasswordHere>';  
GO  
```  

### <a name="b-creating-a-database-scoped-credential-for-a-shared-access-signature"></a>B. 建立資料庫範圍認證的共用的存取簽章。   
下列範例會建立可以用來建立資料庫範圍認證[外部資料來源](../../t-sql/statements/create-external-data-source-transact-sql.md)，可以執行大量作業，例如[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)和[OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md). 共用的存取簽章不能使用 PolyBase，SQL Server、 AP 或 SQL DW 中。
```tsql
CREATE DATABASE SCOPED CREDENTIAL MyCredentials  
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
SECRET = 'QLYMgmSXMklt%2FI1U6DcVrQixnlU5Sgbtk1qDRakUBGs%3D';
```
  
### <a name="c-creating-a-database-scoped-credential-for-polybase-connectivity-to-azure-data-lake-store"></a>C. 建立資料庫範圍認證 PolyBase 連線到 Azure 資料湖存放區。  
下列範例會建立可以用來建立資料庫範圍認證[外部資料來源](../../t-sql/statements/create-external-data-source-transact-sql.md)，這可以由在 Azure SQL 資料倉儲 PolyBase。

Azure 資料湖存放區會進行服務驗證使用 Azure Active Directory 應用程式。
請[建立 AAD 應用程式](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)和記錄 client_id、 OAuth_2.0_Token_EndPoint，與索引鍵，再重新建立資料庫範圍認證。

```tsql
CREATE DATABASE SCOPED CREDENTIAL ADL_User
WITH
    IDENTITY = '<client_id>@\<OAuth_2.0_Token_EndPoint>'
    SECRET = '<key>'
;
```  
  
  
  
## <a name="more-information"></a>詳細資訊  
 [認證 &#40; Database engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  

