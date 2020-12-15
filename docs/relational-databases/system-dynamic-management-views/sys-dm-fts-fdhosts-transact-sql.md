---
description: sys.dm_fts_fdhosts (Transact-SQL)
title: sys.dm_fts_fdhosts (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_fdhosts
- dm_fts_fdhosts_TSQL
- sys.dm_fts_fdhosts
- sys.dm_fts_fdhosts_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_fdhosts dynamic management view
- troubleshooting [SQL Server], full-text search
ms.assetid: d42a6334-4362-4361-83da-f8324fe55ec7
author: pmasl
ms.author: pelopes
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7179f1c12e2ad5363199a644b100783b2addac1a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484690"
---
# <a name="sysdm_fts_fdhosts-transact-sql"></a>sys.dm_fts_fdhosts (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  傳回伺服器執行個體上篩選背景程式主機之目前活動的相關資訊。  
  
 
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**fdhost_id**|**int**|篩選背景程式主機的識別碼。|  
|**fdhost_name**|**nvarchar(120)**|篩選背景程式主機的名稱。|  
|**fdhost_process_id**|**int**|篩選背景程式主機的 Windows 處理序識別碼。|  
|**fdhost_type**|**nvarchar(120)**|篩選背景程式主機正在處理的文件類型，為以下其中一項：<br /><br /> 單一執行緒<br /><br /> 多執行緒<br /><br /> 大型文件|  
|**max_thread**|**int**|篩選背景程式主機中的最大執行緒數目。|  
|**batch_count**|**int**|篩選背景程式主機內正在處理的批次數。|  
  
## <a name="permissions"></a>權限  

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 許可權。   
在 SQL Database Basic、S0 和 S1 服務目標上，以及針對彈性集區中的資料庫，則 `Server admin` `Azure Active Directory admin` 需要或帳戶。 在所有其他 SQL Database 服務目標上， `VIEW DATABASE STATE` 資料庫中都需要有許可權。   

## <a name="examples"></a>範例  
 下列範例會傳回篩選背景程式主機的名稱以及其中的最大執行緒數目。 它也會監視目前在篩選背景程式中處理的批次數。 這項資訊可用來診斷效能。  
  
```  
SELECT fdhost_name, batch_count, max_thread FROM sys.dm_fts_fdhosts;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的全文檢索搜尋和語義搜尋動態管理檢視和函數 ](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [全文檢索搜尋](../../relational-databases/search/full-text-search.md)  
  
  
