---
title: IDBProperties (OLE DB 驅動程式) | Microsoft Docs
description: 了解 OLE DB Driver for SQL Server 中的 IDBProperties 介面，包括 IDBProperties::GetPropertyInfo 方法。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e5122c4f8e78caa4fd28d595a09a58af21aacb4
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861342"
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB 標準規格允許提供者將 VT_EMPTY 指定給 **DBPROPINFO::vValues**。 不過，當您以 **DBPROPSET_ROWSETALL** 呼叫 **IDBProperties::GetPropertyInfo** 擷取資料列集屬性時，OLE DB Driver for SQL Server OLE DB 一律會傳回 VT_EMPTY。  
  
## <a name="see-also"></a>另請參閱  
 [介面 &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
