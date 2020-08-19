---
description: sys.fulltext_semantic_language_statistics_database (Transact-SQL)
title: sys. fulltext_semantic_language_statistics_database (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_semantic_language_statistics_database_TSQL
- fulltext_semantic_language_statistics_database_TSQL
- fulltext_semantic_language_statistics_database
- sys.fulltext_semantic_language_statistics_database
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_semantic_language_statistics_database catalog view
ms.assetid: 32e95614-ed88-4068-8c37-1e21544717bc
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 5c9ec62588251c908b32c4f51d72cc1b8efee4eb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420112"
---
# <a name="sysfulltext_semantic_language_statistics_database-transact-sql"></a>sys.fulltext_semantic_language_statistics_database (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  傳回有關目前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上安裝之語義語言統計資料庫的資料列。  
  
 您可以查詢此檢視表，了解語意處理所需的語義語言統計資料元件。  
   
  
||||  
|-|-|-|  
|**資料行名稱**|**型別**|**說明**|  
|**database_id**|**int**|資料庫的識別碼，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體內是唯一的。|  
|**register_date**|**datetime**|註冊資料庫用於語意處理的日期。|  
|**registered_by**|**int**|註冊資料庫用於語意處理的伺服器主體識別碼。|  
|**version**|**nvarchar(128)**|語義語言統計資料庫特定的最新版本資訊。|  
  
## <a name="general-remarks"></a>一般備註  
 如需詳細資訊，請參閱 [安裝及設定語意搜尋](../../relational-databases/search/install-and-configure-semantic-search.md)。  
  
## <a name="metadata"></a>中繼資料  
 如需有關語義索引所支援之語言的詳細資訊，請查詢目錄檢視 [sys. fulltext_semantic_languages &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md)。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>權限  
 目錄檢視內中繼資料的可見性會限制在使用者所擁有的安全性實體，或已授與使用者某些權限的安全性實體。  
  
## <a name="examples"></a>範例  
 下列範例示範如何查詢 **sys. fulltext_semantic_language_statistics_database** ，以取得目前實例上所註冊之語義語言統計資料庫的相關資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
```  
SELECT * FROM sys.fulltext_semantic_language_statistics_database;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [安裝及設定語意搜尋](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
