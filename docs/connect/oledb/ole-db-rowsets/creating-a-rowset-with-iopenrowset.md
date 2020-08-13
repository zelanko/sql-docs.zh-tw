---
title: 使用 IOpenRowset 建立資料列集 (OLE DB Driver) | Microsoft Docs
description: 使用 OLE DB Driver for SQL Server 的 IOpenRowset 介面建立資料列集
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, creating
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 721a54d4e423675fa5dad39d22e8f94c178228d6
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942378"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>以 IOpenRowset 建立資料列集
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 支援 **IOpenRowset::OpenRowset** 方法，但有下列限制：  
  
-   *pTableID* 參數指向的資料庫識別碼 (DBID) 結構中必須指定基底資料表或檢視表。  
  
-   DBID *eKind* 成員必須指示 DBKIND_NAME。  
  
-   DBID *uName* 成員必須將現有基底資料表或檢視表的名稱指定為 Unicode 字元字串。  
  
-   **OpenRowset** 的 *pIndexID* 參數必須為 NULL。  
  
 **IOpenRowset::OpenRowset** 的結果集包含單一資料列集。 包含單一資料列集的結果集可受到 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料指標的支援。 資料指標支援可讓開發人員使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 並行機制。  
  
## <a name="see-also"></a>另請參閱  
 [資料列集](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
