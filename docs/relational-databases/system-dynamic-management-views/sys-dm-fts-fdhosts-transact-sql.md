---
title: sys.databases dm_fts_fdhosts （Transact-sql） |Microsoft Docs
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1b954e5d9c122f09d1ed16162f34ce94cdbc4100
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734574"
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
在高階 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 層級上，需要 `VIEW DATABASE STATE` 資料庫的許可權。 在 [ [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 標準] 和 [基本] 層上，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。   

## <a name="examples"></a>範例  
 下列範例會傳回篩選背景程式主機的名稱以及其中的最大執行緒數目。 它也會監視目前在篩選背景程式中處理的批次數。 這項資訊可用來診斷效能。  
  
```  
SELECT fdhost_name, batch_count, max_thread FROM sys.dm_fts_fdhosts;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [全文檢索搜尋和語義搜尋動態管理檢視和函數 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [全文檢索搜尋](../../relational-databases/search/full-text-search.md)  
  
  
