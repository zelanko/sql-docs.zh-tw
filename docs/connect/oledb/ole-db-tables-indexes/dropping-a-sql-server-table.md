---
title: 卸除 SQL Server 資料表 |Microsoft 文件
description: 卸除 SQL server 使用 OLE DB 驅動程式的 SQL Server 資料表
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
- tables [OLE DB]
- deleting tables
- OLE DB Driver for SQL Server, tables
- removing tables
- dropping tables
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: b035e65082cc15db2af6f06b636adb0ff388f4ec
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689751"
---
# <a name="dropping-a-sql-server-table"></a>卸除 SQL Server 資料表
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server OLE DB 驅動程式會公開 **:: Droptable**函式以移除[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料庫中的資料表。  
  
 資料表名稱指定為 Unicode 字元字串中*pwszName*隸屬*uName*聯集*Createtable*參數。 *EKind*隸屬*Createtable*必須是 DBKIND_NAME。  
  
## <a name="see-also"></a>另請參閱  
 [資料表和索引](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
