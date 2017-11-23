---
title: "改變外部資料來源 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 11/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL DATA SOURCE
- ALTER_EXTERNAL_DATA_SOURCE
dev_langs: TSQL
helpviewer_keywords:
- polybase, alter external data source statement
- ALTER EXTERNAL DATA SOURCE statement
ms.assetid: a34b9e90-199d-46d0-817a-a7e69387bf5f
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 028a300c8dc6b295a0f10b3cb137809c81c4af95
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="alter-external-data-source-transact-sql"></a>改變外部資料來源 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  修改用來建立外部資料表的外部資料來源。 外部資料來源可以是 Hadoop 或 Azure blob 儲存體 (WASB)。  
  
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
  
 位置 = 'server_name_or_IP' 指定的名稱或 IP 位址的伺服器。
  
 RESOURCE_MANAGER_LOCATION = '\<IP 位址。連接埠 >' 指定的 Hadoop 資源管理員位置。 指定時，查詢最佳化工具可能會選擇前置處理資料的 PolyBase 查詢，利用 Hadoop 的運算功能。 這是成本型決策。 呼叫述詞下推，這可以大幅降低 Hadoop 與 SQL 之間傳送的資料磁碟區，因而改善查詢效能。
  
 認證 = Credential_Name 指定具名的認證。 請參閱[CREATE DATABASE SCOPED CREDENTIAL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).

類型 = BLOB_STORAGE   
**適用於：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]。
針對大量作業，`LOCATION`必須是有效的 Azure Blob 儲存體 URL。 請不要將 **/** 、 檔案名稱，或共用存取簽章參數的結尾`LOCATION`URL。
使用的認證必須使用可建立`SHARED ACCESS SIGNATURE`作為身分識別。 如需共用存取簽章的詳細資訊，請參閱[使用共用存取簽章 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)。

  
  
## <a name="remarks"></a>備註
 可以修改只有單一來源一次。 並行要求修改相同的來源會導致等待一個陳述式。 不過，不同的來源可以修改在相同的時間。 這個陳述式可以與其他陳述式同時執行。
  
## <a name="permissions"></a>Permissions  
 需要 ALTER ANY EXTERNAL DATA SOURCE 權限。
 > [!IMPORTANT]  
 >  ALTER ANY EXTERNAL DATA SOURCE 權限授與任何主體建立和修改任何外部資料來源物件的能力，因此，它也會授與存取在資料庫上的所有資料庫範圍認證的能力。 此權限必須被視為具有高度權限，因此必須只授與信任的主體在系統中。

  
## <a name="examples"></a>範例  
 下列範例會變更的位置和資源管理員位置的現有資料來源。
  
```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET
     LOCATION = 'hdfs://10.10.10.10:8020',
     RESOURCE_MANAGER_LOCATION = '10.10.10.10:8032'
    ;
  
```  

 下列範例會變更要連接到現有的資料來源的認證。
  
```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET
   CREDENTIAL = new_hadoop_user
    ;
```
