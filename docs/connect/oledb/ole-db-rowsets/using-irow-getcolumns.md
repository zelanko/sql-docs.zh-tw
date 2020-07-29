---
title: 使用 IRow::GetColumns | Microsoft Docs
description: 使用 IRow::GetColumns 存取資料列中的所有資料行
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [OLE DB Driver for SQL Server]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 6f00e7c205e559864ed495dccd43f3a4f979260f
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008769"
---
# <a name="using-irowgetcolumns"></a>使用 IRow::GetColumns
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **IRow** 實作可允許以順向循序方式存取資料行。 每次當您存取資料列中的數個資料行時，可以使用 **IRow::GetColumns** 的單一呼叫或是呼叫 **IRow::GetColumns** 多次來存取資料列中的所有資料行。  
  
 **IRow::GetColumns** 的多次呼叫不應該重疊。 例如，如果初次呼叫 **IRow::GetColumns** 會擷取資料行 1、2 和 3，則第二次呼叫 **IRow::GetColumns** 就應該擷取資料行 4、5 和 6。 如果之後的 **IRow::GetColumns** 呼叫重疊，則狀態旗標 (DBCOLUMNACCESS 中的 dwstatus 欄位) 會設定為 DBSTATUS_E_UNAVAILABLE。  
  
## <a name="see-also"></a>另請參閱  
 [使用 IRow 擷取單一資料列](../../oledb/ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
