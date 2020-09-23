---
title: 拖放 SQL Server 索引 (OLE DB Driver) | Microsoft Docs
description: 了解 OLE DB Driver for SQL Server 中的 IIndexDefinition::DropIndex 函式，此函式可讓取用者從 SQL Server 資料表中移除索引。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- removing indexes
- deleting indexes
- DropIndex function
- dropping indexes
- OLE DB Driver for SQL Server, indexes
- indexes [OLE DB]
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 91b9dd9e5ae5978eb8e0290e8d023a0ebca5e9c3
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88858860"
---
# <a name="dropping-a-sql-server-index"></a>卸除 SQL Server 索引
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 會公開 **IIndexDefinition::DropIndex** 函式。 如此可讓取用者從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表中移除索引。  
  
 OLE DB Driver for SQL Server 會公開某些 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PRIMARY KEY 和 UNIQUE 條件約束作為索引。 資料表擁有者、資料庫擁有者以及某些系統管理角色成員都可以修改 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表，卸除條件約束。 根據預設，只有資料表擁有者可以卸除現有的索引。 因此，**DropIndex** 的成功或失敗，不但取決於應用程式使用者的存取權限，也取決於所指出之索引的類型。  
  
 取用者會在 *pTableID* 參數中，將資料表名稱指定為 *uName* 聯集之 *pwszName* 成員中的 Unicode 字元字串。 *pTableID* 的 *eKind* 成員必須是 DBKIND_NAME。  
  
 取用者會在 *pIndexID* 參數中，將索引名稱指定為 *uName* 聯集之 *pwszName* 成員中的 Unicode 字元字串。 *pIndexID* 的 *eKind* 成員必須是 DBKIND_NAME。 當 *pIndexID* 為 Null 時，OLE DB Driver for SQL Server 不支援在資料表上卸除所有索引的 OLE DB 功能。 如果 *pIndexID* 為 Null，會傳回 E_INVALIDARG。  
  
## <a name="see-also"></a>另請參閱  
 [資料表和索引](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-index-transact-sql.md)  
  
  
