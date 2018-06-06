---
title: '使用 irow:: Getcolumns |Microsoft 文件'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
ms.assetid: 1f5d2e03-e6fe-4ea1-b71d-55d02b5d59ae
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b7b32051a7758b47d1c629ccc77773277d088991
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="using-irowgetcolumns"></a>使用 IRow::GetColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **IRow**實作可允許以順向循序方式存取資料行。 您可以存取的資料列的單一呼叫中的所有資料行**irow:: Getcolumns**或呼叫**irow:: Getcolumns**多次，每次您存取數個資料列中的資料行。  
  
 多個呼叫**irow:: Getcolumns**不應該重疊。 例如，如果第一次呼叫**irow:: Getcolumns**擷取資料行 1、 2 和 3，第二次呼叫**irow:: Getcolumns**應該呼叫資料行 4、 5 和 6。 如果稍後呼叫**irow:: Getcolumns**重疊，狀態旗標 （DBCOLUMNACCESS 中的 dwstatus 欄位） 會設定為 DBSTATUS_E_UNAVAILABLE。  
  
## <a name="see-also"></a>另請參閱  
 [擷取單一資料列使用 irow 來](../../relational-databases/native-client-ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
