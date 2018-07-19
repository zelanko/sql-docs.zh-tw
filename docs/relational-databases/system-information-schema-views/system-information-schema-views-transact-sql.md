---
title: 系統資訊結構描述檢視 (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- information schema views
- schemas [SQL Server], information schema views
- metadata [SQL Server], views
- views [SQL Server], information schema
- system views [SQL Server], information schema
ms.assetid: 7e9f1dfe-27e9-40e7-8fc7-bfc5cae6be10
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2a3c0ef6d8a3c4c774b441e807c4ca513b214f26
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33240188"
---
# <a name="system-information-schema-views-transact-sql"></a>系統資訊結構描述檢視 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  資訊結構描述檢視是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用來取得中繼資料的方法之一。 資訊結構描述檢視提供一種與內部系統資料表無關的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中繼資料檢視。 資訊結構描述檢視使應用程式在基礎系統資料表有了重大變更的情況下，仍然能夠正確運作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所包含的資訊結構描述檢視符合 INFORMATION_SCHEMA 的 ISO 標準定義。  
  
> [!IMPORTANT]  
>  資訊結構描述檢視的某些變更會造成無法與舊版相容。 特定檢視的主題會描述這些變更。  
  
 當您參考目前伺服器時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援三部分命名慣例。 另外，ISO 標準也支援三部分命名慣例。 不過，兩種命名慣例所用的名稱不同。 資訊結構描述檢視定義在名稱為 INFORMATION_SCHEMA 的特殊結構描述中。 每個資料庫都包含這個結構描述。 每份資訊結構描述檢視都包含這個特定資料庫所儲存的所有資料物件。 下表顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名稱和 SQL 標準名稱之間的關聯性。  
  
|SQL Server 名稱|對應至這個相等的 SQL 標準名稱|  
|---------------------|-----------------------------------------------|  
|資料庫|目錄|  
|結構描述|結構描述|  
|物件|物件|  
|使用者自訂資料類型|網域|  
  
 這個名稱對應慣例適用於下列與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ISO 相容的檢視。  
  
|||  
|-|-|  
|[CHECK_CONSTRAINTS](../../relational-databases/system-information-schema-views/check-constraints-transact-sql.md)|[REFERENTIAL_CONSTRAINTS](../../relational-databases/system-information-schema-views/referential-constraints-transact-sql.md)|  
|[COLUMN_DOMAIN_USAGE](../../relational-databases/system-information-schema-views/column-domain-usage-transact-sql.md)|[ROUTINES](../../relational-databases/system-information-schema-views/routines-transact-sql.md)|  
|[COLUMN_PRIVILEGES](../../relational-databases/system-information-schema-views/column-privileges-transact-sql.md)|[ROUTINE_COLUMNS](../../relational-databases/system-information-schema-views/routine-columns-transact-sql.md)|  
|[COLUMNS](../../relational-databases/system-information-schema-views/columns-transact-sql.md)|[SCHEMATA](../../relational-databases/system-information-schema-views/schemata-transact-sql.md)|  
|[CONSTRAINT_COLUMN_USAGE](../../relational-databases/system-information-schema-views/constraint-column-usage-transact-sql.md)|[TABLE_CONSTRAINTS](../../relational-databases/system-information-schema-views/table-constraints-transact-sql.md)|  
|[CONSTRAINT_TABLE_USAGE](../../relational-databases/system-information-schema-views/constraint-table-usage-transact-sql.md)|[TABLE_PRIVILEGES](../../relational-databases/system-information-schema-views/table-privileges-transact-sql.md)|  
|[DOMAIN_CONSTRAINTS](../../relational-databases/system-information-schema-views/domain-constraints-transact-sql.md)|[TABLES](../../relational-databases/system-information-schema-views/tables-transact-sql.md)|  
|[DOMAINS](../../relational-databases/system-information-schema-views/domains-transact-sql.md)|[VIEW_COLUMN_USAGE](../../relational-databases/system-information-schema-views/view-column-usage-transact-sql.md)|  
|[KEY_COLUMN_USAGE](../../relational-databases/system-information-schema-views/key-column-usage-transact-sql.md)|[VIEW_TABLE_USAGE](../../relational-databases/system-information-schema-views/view-table-usage-transact-sql.md)|  
|[PARAMETERS](../../relational-databases/system-information-schema-views/parameters-transact-sql.md)|[VIEWS](../../relational-databases/system-information-schema-views/views-transact-sql.md)|  
  
 另外，部分檢視也會包含不同資料類別的參考，如字元資料或二進位資料。  
  
 當您參考資訊結構描述檢視時，您必須使用包含 `INFORMATION_SCHEMA` 結構描述名稱的限定名稱。 例如：  
  
```  
SELECT TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME, COLUMN_NAME, COLUMN_DEFAULT  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = N'Product';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統檢視表&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
