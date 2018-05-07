---
title: IDBProperties (OLE DB) |Microsoft 文件
description: IDBProperties 介面 (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 6abe81b7f149f3018872d7e3aa89b90a315dc628
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB 標準規格允許提供者將 VT_EMPTY 指定給**DBPROPINFO::vValues**。 不過，OLE DB 驅動程式的 SQL Server OLE DB 一定會傳回 VT_EMPTY 當您呼叫**idbproperties:: Getpropertyinfo**與**DBPROPSET_ROWSETALL**來擷取資料列集屬性。  
  
## <a name="see-also"></a>另請參閱  
 [介面 & #40; OLE DB & #41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
