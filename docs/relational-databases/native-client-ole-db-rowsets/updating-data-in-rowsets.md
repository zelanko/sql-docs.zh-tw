---
description: 更新 SQL Server Native Client 中資料列集的資料
title: '更新資料列集中的資料 (Native Client OLE DB 提供者) '
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- rowsets [OLE DB], updating data
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, updating data
- SQL Server Native Client OLE DB provider, data updates
- data updates [SQL Server], OLE DB
ms.assetid: 37769b1c-c480-419a-8c54-5cc420bf73db
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 079145525b401831ea163c1208c69d7e0e172c9d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448330"
---
# <a name="updating-data-in-rowsets-in-sql-server-native-client"></a>更新 SQL Server Native Client 中資料列集的資料
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當取用者更新包含該資料的可修改資料列集時，Native Client OLE DB provider 會更新資料。 當取用者要求 **IRowsetChange** 或 **IRowsetUpdate** 介面的支援時，就會建立可修改的資料列集。  
  
 所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者可修改的資料列集都會使用資料 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指標來支援資料列集。 資料列集屬性 DBPROP_LOCKMODE 會改變資料指標中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並行控制行為，並且決定可更新資料列集中的資料列集資料列擷取以及資料完整性錯誤產生的行為。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 OLE DB 提供者支援更新之前或之後的資料列同步處理。  
  
> [!NOTE]  
>  IRowChange::SetColumns 可用來設定資料列物件的一或多個具名資料行的值。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [更新 SQL Server 資料指標中的資料](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-sql-server-cursors.md)  
  
-   [重新同步處理資料列](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料列集](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
