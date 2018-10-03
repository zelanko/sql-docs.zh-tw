---
title: 重新同步處理的資料列 |Microsoft Docs
description: 使用 OLE DB Driver for SQL Server 的重新同步處理資料列
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: d50246e596472e2835add790101d92482161c02a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47657786"
---
# <a name="updating-data-in-rowsets---resynchronizing-rows"></a>更新資料列集中的資料 - 重新同步處理資料列
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 支援**IRowsetResynch**上[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料指標支援資料列集僅。 **IRowsetResynch** 無法視需要提供。 取用者必須在開啟資料列集前要求此介面。  
  
## <a name="see-also"></a>另請參閱  
 [更新資料列集中的資料](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
