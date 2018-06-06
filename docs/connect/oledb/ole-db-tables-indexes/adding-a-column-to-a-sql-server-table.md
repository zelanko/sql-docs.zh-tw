---
title: SQL Server 資料表中加入一個資料行 |Microsoft 文件
description: 使用 SQL Server 的 OLE DB 驅動程式的 SQL Server 資料表中加入一個資料行
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-tables-indexes
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
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 2f49f014e29401d0f99bd5f9bd59551c94255399
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="adding-a-column-to-a-sql-server-table"></a>將資料行加入至 SQL Server 資料表
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL Server OLE DB 驅動程式會公開 **:: Addcolumn**函式。 這可讓取用者加入至資料行[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料表。  
  
 當您將加入的資料行[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料表、 OLE DB 驅動程式的 SQL Server 取用者會受到限制，如下所示：  
  
-   如果 DBPROP_COL_AUTOINCREMENT 是 VARIANT_TRUE，DBPROP_COL_NULLABLE 就必須是 VARIANT_FALSE。  
  
-   如果資料行定義使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**時間戳記**資料類型，dbprop_col_nullable 就必須是 VARIANT_FALSE。  
  
-   如果是其他任何資料行定義，DBPROP_COL_NULLABLE 必須為 VARIANT_TRUE。  
  
 取用者指定的資料表名稱中的 Unicode 字元字串*pwszName*隸屬*uName*聯集*Createtable*參數。 *EKind*隸屬*Createtable*必須是 DBKIND_NAME。  
  
 新的資料行名稱指定為 Unicode 字元字串中*pwszName*隸屬*uName*聯集*pwszname*之 DBCOLUMNDESC 參數成員*Pwszname*。 *EKind*成員必須是 DBKIND_NAME。  
  
## <a name="see-also"></a>另請參閱  
 [資料表和索引](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)  
  
  
