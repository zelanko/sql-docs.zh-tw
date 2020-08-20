---
description: '使用 IOpenRowset 建立資料列集 (Native Client OLE DB 提供者) '
title: 建立具有 IOpenRowset (Native Client OLE DB provider) 的資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1b6d6d554c6ac0335ec0504886ea7e8de06437f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499127"
---
# <a name="creating-a-rowset-with-iopenrowset-in-sql-server-native-client"></a>在 SQL Server Native Client 中使用 IOpenRowset 建立資料列集
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB provider 支援**IOpenRowset：： OpenRowset**方法，但有下列限制：  
  
-   *pTableID* 參數指向的資料庫識別碼 (DBID) 結構中必須指定基底資料表或檢視表。  
  
-   DBID *eKind* 成員必須指示 DBKIND_NAME。  
  
-   DBID *uName* 成員必須將現有基底資料表或檢視表的名稱指定為 Unicode 字元字串。  
  
-   **OpenRowset** 的 *pIndexID* 參數必須為 NULL。  
  
 **IOpenRowset::OpenRowset** 的結果集包含單一資料列集。 包含單一資料列集的結果集可受到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料指標的支援。 資料指標支援可讓開發人員使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並行機制。  
  
## <a name="see-also"></a>另請參閱  
 [資料列集](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
