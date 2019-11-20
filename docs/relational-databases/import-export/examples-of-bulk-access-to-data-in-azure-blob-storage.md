---
title: 大量存取 Azure Blob 儲存體中的資料
ms.description: Transact-SQL examples that use BULK INSERT and OPENROWSET to access data in an Azure Blob storage account.
ms.date: 10/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], from Azure blob storage
- Azure blob storage, bulk import to SQL Server
- BULK INSERT, Azure blob storage
- OPENROWSET, Azure blob storage
ms.assetid: f7d85db3-7a93-400e-87af-f56247319ecd
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: 08e81abbc21671881affc80fc9b7f0346cd490f7
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056009"
---
# <a name="examples-of-bulk-access-to-data-in-azure-blob-storage"></a>大量存取 Azure Blob 儲存體中資料的範例

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

`BULK INSERT` 和 `OPENROWSET` 陳述式可以直接存取 Azure Blob 儲存體中的檔案。 下列範例會使用 CSV (逗號分隔值) 檔案 (名為 `inv-2017-01-19.csv`)、容器 (名為 `Week3`) 中所儲存或儲存體帳戶 (名為 `newinvoices`) 中所儲存的資料。 您可以使用格式檔案的路徑，但該檔案未包括在這些範例中。

從 SQL Server 大量存取 Azure Blob 儲存體，需要至少 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1。

> [!IMPORTANT]
> 容器和 Blob 上檔案的所有路徑都是 `CASE SENSITIVE`。 如果不正確，可能會傳回錯誤，例如「無法大量載入。 沒有檔案 "file.csv"，或您不具檔案存取權限。」

## <a name="create-the-credential"></a>建立認證

下列所有範例都需要參考一個共用存取簽章的資料庫範圍認證。

> [!IMPORTANT]
> 必須透過使用 `SHARED ACCESS SIGNATURE` 識別的資料庫範圍認證建立外部資料來源。 若要建立儲存體帳戶的共用存取簽章，請參閱 Azure 入口網站之儲存體帳戶屬性頁面上的 [共用存取簽章]  屬性。 如需共用存取簽章的詳細資訊，請參閱[使用共用存取簽章 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)。 如需認證的詳細資訊，請參閱 [CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)。

使用必須為 `SHARED ACCESS SIGNATURE` 的 `IDENTITY` 建立資料庫範圍認證。 使用針對 Blob 儲存體帳戶所產生的 SAS 權杖。 請確認您的 SAS 權杖沒有前置 `?`、您至少擁有應載入物件的讀取權限，以及到期期間是否有效 (所有日期都是 UTC 時間)。

例如：

```sql
CREATE DATABASE SCOPED CREDENTIAL UploadInvoices
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
SECRET = 'sv=2018-03-28&ss=b&srt=sco&sp=rwdlac&se=2019-08-31T02:25:19Z&st=2019-07-30T18:25:19Z&spr=https&sig=KS51p%2BVnfUtLjMZtUTW1siyuyd2nlx294tL0mnmFsOk%3D';
```

## <a name="accessing-data-in-a-csv-file-referencing-an-azure-blob-storage-location"></a>存取參考 Azure Blob 儲存體位置之 CSV 檔案中的資料

下列範例會使用指向名為 `MyAzureInvoices` 之 Azure 儲存體帳戶的外部資料來源。

```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net',
        CREDENTIAL = UploadInvoices
    );
```

接著，`OPENROWSET` 陳述式將容器名稱 (`week3`) 新增至檔案描述。 檔案命名為 `inv-2017-01-19.csv`。

```sql
SELECT * FROM OPENROWSET(
   BULK 'week3/inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoices',
   FORMAT = 'CSV',
   FORMATFILE='invoices.fmt',
   FORMATFILE_DATA_SOURCE = 'MyAzureInvoices'
   ) AS DataFile;   
```

使用 `BULK INSERT` 時，請使用容器和檔案描述︰

```sql
BULK INSERT Colors2
FROM 'week3/inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoices',
      FORMAT = 'CSV');
```

## <a name="accessing-data-in-a-csv-file-referencing-a-container-in-an-azure-blob-storage-location"></a>存取參考 Azure Blob 儲存體位置中容器之 CSV 檔案中的資料

下列範例會使用指向 Azure 儲存體帳戶中容器 (名為 `week3`) 的外部資料來源。

```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoicesContainer
    WITH (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3',
        CREDENTIAL = UploadInvoices
    );
```

接著，`OPENROWSET` 陳述式不會將容器名稱包含在檔案描述中：

```sql
SELECT * FROM OPENROWSET(
   BULK 'inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoicesContainer',
   FORMAT = 'CSV',
   FORMATFILE='invoices.fmt',
   FORMATFILE_DATA_SOURCE = 'MyAzureInvoices'
   ) AS DataFile;
```

使用 `BULK INSERT` 時，請不要使用檔案描述中的容器名稱︰

```sql
BULK INSERT Colors2
FROM 'inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoicesContainer',
      FORMAT = 'CSV');
```

## <a name="see-also"></a>另請參閱

- [CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)
- [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)
- [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)
