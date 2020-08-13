---
title: 使用 IRow 擷取單一資料列 (OLE DB 驅動程式) | Microsoft Docs
description: 使用 OLE DB Driver for SQL Server 的 IRow 介面來擷取單一資料列
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
- OLE DB Driver for SQL Server, fetching
author: pmasl
ms.author: pelopes
ms.openlocfilehash: fba517134c69914914da95daacafdf634de7b15c
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87244242"
---
# <a name="fetching-a-single-row-with-irow-ole-db-driver"></a>使用 IRow 擷取單一資料列 (OLE DB 驅動程式)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  為了提升效能，OLE DB Driver for SQL Server 中的 **IRow** 介面實作已簡化。 **IRow** 允許直接存取單一資料列物件的資料行。 如果您事先知道命令執行的結果只會產生單一資料列，**IRow** 就會擷取該資料列的資料行。 如果結果集包含多個資料列，**IRow** 就只會公開第一個資料列。  
  
 **IRow** 實作不允許資料列的任何導覽。 此資料列中的每個資料行只會存取一次，但有一項例外狀況：您可以存取一次資料行來尋找資料行大小，然後再次存取，以便提取資料。  
  
> [!NOTE]  
>  **IRow::Open** 僅支援開啟 DBGUID_STREAM 和 DBGUID_NULL 類型的物件。  
  
 若要使用 **ICommand::Execute** 方法來取得資料列物件，您必須傳遞 IID_IRow。 **IMultipleResults** 介面必須用來處理多個結果集。 **IMultipleResults** 支援 **IRow** 和 **IRowset**。 **IRowset** 可用於大量作業。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [使用 IRow::GetColumns](../../oledb/ole-db-rowsets/using-irow-getcolumns.md)   
  
## <a name="see-also"></a>另請參閱  
 [資料列集](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
