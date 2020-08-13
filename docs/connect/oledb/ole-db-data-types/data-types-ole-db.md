---
title: 資料類型 (OLE DB 驅動程式) | Microsoft Docs
description: 資料類型 (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- OLE DB Driver for SQL Server, data types
- data types [OLE DB]
- OLE DB, data types
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 28ff4bfc3262803ba8bafcb405e477a1692cb93f
ms.sourcegitcommit: 08f331b6a5fe72d68ef1b2eccc5d16cb80c6ee39
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "86977748"
---
# <a name="data-types-ole-db"></a>資料類型 (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  若要使用 OLE DB Driver for SQL Server 來執行 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式並處理結果，您必須知道 OLE DB Driver for SQL Server 在繫結資料列集中的參數或資料行時，如何將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型對應至 OLE DB 資料類型，以及它使用 **ITableDefinition** 介面在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中建立資料表的時機。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [資料列集和參數中的資料類型對應](../../oledb/ole-db-data-types/data-type-mapping-in-rowsets-and-parameters.md)  
  
-   [ITableDefinition 中的資料類型對應](../../oledb/ole-db-data-types/data-type-mapping-in-itabledefinition.md)  
  
-   [SSVARIANT 結構](../../oledb/ole-db-data-types/ssvariant-structure.md)  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 程式設計](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
