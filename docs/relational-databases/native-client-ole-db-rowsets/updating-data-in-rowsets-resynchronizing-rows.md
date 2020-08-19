---
description: 更新資料列集中的資料-重新同步處理 SQL Server Native Client 中的資料列
title: " (Native Client OLE DB 提供者重新同步處理資料列) "
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
ms.assetid: d2d30505-a878-4aa9-b821-53d8118a45a5
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 65f077141e6e29e3f524f8ac183e5f624b187319
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448337"
---
# <a name="updating-data-in-rowsets---resynchronizing-rows-in-sql-server-native-client"></a>更新資料列集中的資料-重新同步處理 SQL Server Native Client 中的資料列
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 OLE DB 提供者僅支援在資料指標支援的資料列集上**IRowsetResynch** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 **IRowsetResynch** 無法視需要提供。 取用者必須在開啟資料列集前要求此介面。  
  
## <a name="see-also"></a>另請參閱  
 [更新資料列集中的資料](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
