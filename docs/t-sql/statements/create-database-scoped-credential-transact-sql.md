---
title: CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=aps-pdw-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2fff507046ae5a53abbffbd91bb245f52d57a53c
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594142"
---
# <a name="create-database-scoped-credential-transact-sql"></a>CREATE DATABASE SCOPED CREDENTIAL (TRANSACT-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

建立資料庫認證。 資料庫認證未對應到伺服器登入或資料庫使用者。 每當資料庫執行需要存取權的作業時，資料庫就會使用該認證存取外部位置。

![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>語法

``` 
CREATE DATABASE SCOPED CREDENTIAL credential_name
WITH IDENTITY = 'identity_name'
    [ , SECRET = 'secret' ]

```

## <a name="arguments"></a>引數

*credential_name* 指定要所建立資料庫範圍認證的名稱。 *credential_name* 的開頭不可以是編號 (#) 符號。 系統認證必須以 ## 為開頭。

IDENTITY **='** _identity\_name_ **'** 指定連接到伺服器外部時所要使用的帳戶名稱。 若要使用共用金鑰從 Azure Blob 儲存體匯入檔案，身分識別名稱必須為 `SHARED ACCESS SIGNATURE`。 若要將資料載入 SQL DW，可以將任何有效值用於身分識別。 如需共用存取簽章的詳細資訊，請參閱[使用共用存取簽章 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)。

SECRET **='** _secret_ **'** 指定外寄驗證所需的祕密。 從 Azure Blob 儲存體匯入檔案需要 `SECRET`。 若要從 Azure Blob 儲存體載入到 SQL DW 或平行處理資料倉儲，祕密必須是Azure 儲存體金鑰。
> [!WARNING]
> SAS 金鑰值的開頭可能是 '?' (問號)。 當您使用 SAS 金鑰時，您必須移除前置字元 '?'。 否則您的工作可能會受阻。

## <a name="remarks"></a>Remarks

資料庫範圍認證是包含驗證資訊的資料列，該資訊是連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 外部資源時所需的資訊。 大部分認證都包含 Windows 使用者和密碼。

在建立資料庫範圍認證之前，資料庫必須具有保護認證的主要金鑰。 如需詳細資訊，請參閱 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)。

當 IDENTITY 是 Windows 使用者時，秘密可以是密碼。 秘密是利用服務主要金鑰來加密的。 如果重新產生服務主要金鑰，便會利用新的服務主要金鑰來重新加密秘密。

資料庫範圍認證的相關資訊顯示在 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) 目錄檢視中。

下列是一些資料庫範圍認證的應用程式：

- [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 使用資料庫範圍認證來存取非公開 Azure Blob 儲存體或含 PolyBase 受 Kerberos 保護的 Hadoop 叢集。 若要深入了解，請參閱 [CREATE EXTERNAL DATA SOURCE (TRANSACT-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)。

- [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] 使用資料庫範圍認證來存取含 PolyBase 的非公開 Azure Blob 儲存體。 若要深入了解，請參閱 [CREATE EXTERNAL DATA SOURCE (TRANSACT-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)。

- [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 針對其全域查詢功能使用資料庫範圍認證。 這是跨多個資料庫分區查詢的功能。

- [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 使用資料庫範圍認證將擴充事件檔案寫入 Azure Blob 儲存體。

- [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 將資料庫範圍認證用於彈性集區。 如需詳細資訊，請參閱[彈性集區可協助您管理及調整多個 Azure SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)

- [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 和 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) 使用資料庫範圍認證存取 Azure Blob 儲存體的資料。 如需詳細資訊，請參閱[大量存取 Azure Blob 儲存體資料的範例](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md)。 

## <a name="permissions"></a>權限

需要資料庫上的 **CONTROL** 權限。

## <a name="examples"></a>範例

### <a name="a-creating-a-database-scoped-credential-for-your-application"></a>A. 為您的應用程式建立資料庫範圍認證

下列範例會建立稱為 `AppCred` 的資料庫範圍認證。 該資料庫範圍認證包含 Windows 使用者 `Mary5` 和密碼。

```sql
-- Create a db master key if one does not already exist, using your own password.
CREATE MASTER KEY ENCRYPTION BY PASSWORD='<EnterStrongPasswordHere>';

-- Create a database scoped credential.
CREATE DATABASE SCOPED CREDENTIAL AppCred WITH IDENTITY = 'Mary5',
    SECRET = '<EnterStrongPasswordHere>';
```

### <a name="b-creating-a-database-scoped-credential-for-a-shared-access-signature"></a>B. 建立共用存取簽章的資料庫範圍認證

下列範例會建立可用於建立[外部資料來源](../../t-sql/statements/create-external-data-source-transact-sql.md)的資料庫範圍認證，可進行 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 和 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) 等大量作業。 「共用存取簽章」不能在 SQL Server、APS 或 SQL DW 中與 PolyBase 搭配使用。

```sql
-- Create a db master key if one does not already exist, using your own password.
CREATE MASTER KEY ENCRYPTION BY PASSWORD='<EnterStrongPasswordHere>';

-- Create a database scoped credential.CREATE DATABASE SCOPED CREDENTIAL MyCredentials
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
SECRET = 'QLYMgmSXMklt%2FI1U6DcVrQixnlU5Sgbtk1qDRakUBGs%3D';
```

### <a name="c-creating-a-database-scoped-credential-for-polybase-connectivity-to-azure-data-lake-store"></a>C. 建立可讓 PolyBase 連線到 Azure Data Lake Store 的資料庫範圍認證

下列範例會建立可以用於建立[外部資料來源](../../t-sql/statements/create-external-data-source-transact-sql.md) (可在 Azure SQL 資料倉儲中供 PolyBase 使用) 的資料庫範圍認證。

Azure Data Lake Store 將 Azure Active Directory 應用程式用於「服務對服務驗證」。
請先[建立 AAD 應用程式](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)並記錄您的 client_id、OAuth_2.0_Token_EndPoint 和金鑰，然後再嘗試建立資料庫範圍認證。

```sql
-- Create a db master key if one does not already exist, using your own password.
CREATE MASTER KEY ENCRYPTION BY PASSWORD='<EnterStrongPasswordHere>';

-- Create a database scoped credential.
CREATE DATABASE SCOPED CREDENTIAL ADL_User
WITH
    IDENTITY = '<client_id>@\<OAuth_2.0_Token_EndPoint>',
    SECRET = '<key>'
;
```

## <a name="more-information"></a>詳細資訊

- [認證 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)
- [ALTER DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)
- [DROP DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)
- [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)
- [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)
- [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
