---
title: ALTER EXTERNAL DATA SOURCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL DATA SOURCE
- ALTER_EXTERNAL_DATA_SOURCE
dev_langs:
- TSQL
helpviewer_keywords:
- polybase, alter external data source statement
- ALTER EXTERNAL DATA SOURCE statement
ms.assetid: a34b9e90-199d-46d0-817a-a7e69387bf5f
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 71a88e2909a1f335dbf6014aa8d53a1e0b08c93b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47667246"
---
# <a name="alter-external-data-source-transact-sql"></a>ALTER EXTERNAL DATA SOURCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  修改用來建立外部資料表的外部資料來源。 外部資料來源可以是 Hadoop 或 Azure Blob 儲存體 (WASB)。
  
## <a name="syntax"></a>語法  
  
```  
-- Modify an external data source
-- Applies to: SQL Server (2016 or later)
ALTER EXTERNAL DATA SOURCE data_source_name SET
    {   
        LOCATION = 'server_name_or_IP' [,] |
        RESOURCE_MANAGER_LOCATION = <'IP address;Port'> [,] |
        CREDENTIAL = credential_name
    }  
    [;]  

-- Modify an external data source pointing to Azure Blob storage
-- Applies to: SQL Server (starting with 2017)
ALTER EXTERNAL DATA SOURCE data_source_name
    WITH (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://storage_account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ]
    )  
```  
  
## <a name="arguments"></a>引數  
 data_source_name 指定資料來源的使用者定義名稱。 名稱必須是唯一的。
  
 LOCATION = ‘server_name_or_IP’ 指定伺服器名稱或 IP 位址。
  
 RESOURCE_MANAGER_LOCATION = ‘\<IP address;Port>’ 指定 Hadoop 資源管理員位置。 指定時，查詢最佳化工具可能會使用 Hadoop 的計算功能，選擇對適用於 PolyBase 查詢的資料進行前置處理。 這是成本型決策。 稱為述詞下推，這可大幅降低在 Hadoop 與 SQL 之間傳送的資料量，因而改善查詢效能。
  
 CREDENTIAL = Credential_Name 指定具名認證。 請參閱 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)。

TYPE = BLOB_STORAGE   
**適用於：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]。
僅適用於大量作業，`LOCATION` 必須是有效的 Azure Blob 儲存體 URL。 不要將 **/**、檔案名稱或共用存取簽章參數放置於 `LOCATION` URL 的結尾處。
使用的認證必須利用 `SHARED ACCESS SIGNATURE` 來建立，以作為身分識別。 如需共用存取簽章的詳細資訊，請參閱[使用共用存取簽章 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)。

  
  
## <a name="remarks"></a>Remarks
 每次只能修改單一來源。 修改相同來源的同時要求會導致一個陳述式進入等待。 不過，可同時修改不同的來源。 這個陳述式可以與其他陳述式同時執行。
  
## <a name="permissions"></a>[權限]  
 要求 ALTER ANY EXTERNAL DATA SOURCE 權限。
 > [!IMPORTANT]  
 >  ALTER ANY EXTERNAL DATA SOURCE 權限可讓任何主體都能夠建立及修改任何外部資料來源物件，因此也會讓主體能夠存取資料庫上的所有資料庫範圍認證。 必須將此權限視為具高度權限，因此必須僅授與系統中受信任的主體。

  
## <a name="examples"></a>範例  
 下列範例會改變現有資料來源的位置和資源管理員位置。
  
```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET
     LOCATION = 'hdfs://10.10.10.10:8020',
     RESOURCE_MANAGER_LOCATION = '10.10.10.10:8032'
    ;
  
```  

 下列範例會改變要連線到現有資料來源的認證。
  
```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET
   CREDENTIAL = new_hadoop_user
    ;
```
