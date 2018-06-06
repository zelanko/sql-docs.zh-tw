---
title: 重新同步處理資料列 |Microsoft 文件
description: 使用 SQL Server 的 OLE DB 驅動程式的重新同步處理資料列
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: cda60f254d200e6e8c23235bdeb9988b2dd80309
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="updating-data-in-rowsets---resynchronizing-rows"></a>更新資料列集的重新同步處理資料列中的資料
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL Server 的 OLE DB 驅動程式支援**IRowsetResynch**上[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料指標支援資料列集僅。 **IRowsetResynch**並不適用於要求。 取用者必須在開啟資料列集前要求此介面。  
  
## <a name="see-also"></a>另請參閱  
 [更新資料集中的資料列集](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
