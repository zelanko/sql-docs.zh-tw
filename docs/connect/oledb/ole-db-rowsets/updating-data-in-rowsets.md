---
title: 更新資料列集中 |Microsoft Docs
description: 更新資料集中的資料列集使用 OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- rowsets [OLE DB], updating data
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, updating data
- OLE DB Driver for SQL Server, data updates
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 5d04dd365c3c25a91373c0d23a4acaaf77d204e3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809906"
---
# <a name="updating-data-in-rowsets"></a>更新資料列集中的資料
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  當取用者更新包含 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料的可修改資料列集時，OLE DB Driver for SQL Server 會更新該資料。 當取用者要求 **IRowsetChange** 或 **IRowsetUpdate** 介面的支援時，就會建立可修改的資料列集。  
  
 所有 OLE DB Driver for SQL Server 可修改的資料列集使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料指標來支援資料列集。 資料列集屬性 DBPROP_LOCKMODE 會改變資料指標中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 並行控制行為，並且決定可更新資料列集中的資料列集資料列擷取以及資料完整性錯誤產生的行為。  
  
 OLE DB Driver for SQL Server 支援更新前後的資料列同步處理。  
  
> [!NOTE]  
>  IRowChange::SetColumns 可用來設定資料列物件的一或多個具名資料行的值。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [更新 SQL Server 資料指標中的資料](../../oledb/ole-db-rowsets/updating-data-in-sql-server-cursors.md)  
  
-   [重新同步處理資料列](../../oledb/ole-db-rowsets/updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料列集](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
