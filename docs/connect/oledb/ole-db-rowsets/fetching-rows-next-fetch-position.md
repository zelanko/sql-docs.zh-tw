---
title: 下一個擷取位置 (OLE DB driver) | Microsoft Docs
description: OLE DB Driver for SQL Server 會追蹤下一個擷取位置，讓一連串對 GetNextRows 方法的呼叫讀取整個資料列集。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0ba713e9da40255d992e7cccf8c8430a205cadf4
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861585"
---
# <a name="fetching-rows---next-fetch-position-ole-db-driver"></a>擷取資料列 - 下一個擷取位置 (OLE DB Driver)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 會追蹤下一個提取位置，讓 **GetNextRows** 方法的呼叫序列 (沒有略過、變更方向，或者介入 **FindNextRow**、**Seek** 或 **RestartPosition** 方法的呼叫) 讀取完整的資料列集，而不用略過或重複任何資料列。 下一個提取位置的變更方式為：呼叫 **IRowset::GetNextRows**、**IRowset::RestartPosition** 或 **IRowsetIndex::Seek**，或者呼叫包含 Null *pBookmark* 值的 **FindNextRow**。 呼叫包含非 Null *pBookmark* 值的 **FindNextRow** 不會影響下一個提取位置。  
  
## <a name="see-also"></a>另請參閱  
 [擷取資料列](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
  
