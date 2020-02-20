---
title: IDBProperties (OLE DB) | Microsoft Docs
description: IDBProperties 介面 (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: d8515ef92ce1284379327e63a4bd1730577bd8df
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67994481"
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB 標準規格允許提供者將 VT_EMPTY 指定給 **DBPROPINFO::vValues**。 不過，當您以 **DBPROPSET_ROWSETALL** 呼叫 **IDBProperties::GetPropertyInfo** 擷取資料列集屬性時，OLE DB Driver for SQL Server OLE DB 一律會傳回 VT_EMPTY。  
  
## <a name="see-also"></a>另請參閱  
 [介面 &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
