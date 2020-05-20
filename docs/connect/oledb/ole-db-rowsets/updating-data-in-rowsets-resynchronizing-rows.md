---
title: 重新同步處理資料列 | Microsoft Docs
description: 使用 OLE DB Driver for SQL Server 重新同步處理資料列
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
ms.openlocfilehash: 2f1ea1a563e986914c5fe820740776da129c3b28
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67994168"
---
# <a name="updating-data-in-rowsets---resynchronizing-rows"></a>更新資料列集中的資料 - 重新同步資料列
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 僅支援 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料指標支援之資料列集上的 **IRowsetResynch**。 **IRowsetResynch** 無法視需要提供。 取用者必須在開啟資料列集前要求此介面。  
  
## <a name="see-also"></a>另請參閱  
 [更新資料列集中的資料](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
