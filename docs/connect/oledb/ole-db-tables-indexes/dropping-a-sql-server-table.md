---
title: 卸除 SQL Server 資料表 | Microsoft Docs
description: 使用 OLE DB Driver for SQL Server 卸載 SQL Server 資料表
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- deleting tables
- OLE DB Driver for SQL Server, tables
- removing tables
- dropping tables
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 5c5b241af215c04a72bf389079a4a0299d7496b7
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67994001"
---
# <a name="dropping-a-sql-server-table"></a>卸除 SQL Server 資料表
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 會公開 **ITableDefinition::DropTable** 函式，以從資料庫移除 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表。  
  
 在 *pTableID* 參數中，將資料表名稱指定為 *uName* 聯集之 *pwszName* 成員中的 Unicode 字元字串。 *pTableID* 的 *eKind* 成員必須是 DBKIND_NAME。  
  
## <a name="see-also"></a>另請參閱  
 [資料表和索引](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
