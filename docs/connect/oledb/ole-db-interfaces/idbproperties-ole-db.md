---
title: IDBProperties (OLE DB) |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 7fc3b594224c4f8a664e6ff44398697581c99a4c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802493"
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB 標準規格允許提供者將 VT_EMPTY 指定給 **DBPROPINFO::vValues**。 不過，OLE DB Driver for SQL Server OLE DB 一定會傳回 VT_EMPTY 當您呼叫**idbproperties:: Getpropertyinfo**具有**DBPROPSET_ROWSETALL**來擷取資料列集屬性。  
  
## <a name="see-also"></a>另請參閱  
 [介面&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
