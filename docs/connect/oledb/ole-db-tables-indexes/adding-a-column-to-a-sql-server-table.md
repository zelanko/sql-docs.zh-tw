---
title: 加入 SQL Server 資料表中的資料行 |Microsoft Docs
description: 使用 OLE DB Driver for SQL Server 的 SQL Server 資料表中加入一個資料行
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- AddColumn function
- OLE DB Driver for SQL Server, columns
- adding columns
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 65ac05fb361e3308304bf8457c036d68cc610501
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43020882"
---
# <a name="adding-a-column-to-a-sql-server-table"></a>將資料行加入至 SQL Server 資料表
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 會公開**itabledefinition:: Addcolumn**函式。 如此可讓取用者將資料行加入至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表。  
  
 當您將加入的資料行[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料表，OLE DB Driver for SQL Server 取用者受到限制，如下所示：  
  
-   如果 DBPROP_COL_AUTOINCREMENT 是 VARIANT_TRUE，DBPROP_COL_NULLABLE 就必須是 VARIANT_FALSE。  
  
-   如果資料行是使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **timestamp** 資料類型所定義，DBPROP_COL_NULLABLE 就必須是 VARIANT_FALSE。  
  
-   如果是其他任何資料行定義，DBPROP_COL_NULLABLE 必須為 VARIANT_TRUE。  
  
 取用者會在 *pTableID* 參數中，將資料表名稱指定為 *uName* 聯集之 *pwszName* 成員中的 Unicode 字元字串。 *pTableID* 的 *eKind* 成員必須是 DBKIND_NAME。  
  
 在 *pColumnDesc* 之 DBCOLUMNDESC 參數的 *dbcid* 成員中，新的資料行名稱會指定為 *uName* 聯集之 *pwszName* 成員內的 Unicode 字元字串。 *eKind* 成員必須是 DBKIND_NAME。  
  
## <a name="see-also"></a>另請參閱  
 [資料表和索引](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)  
  
  
