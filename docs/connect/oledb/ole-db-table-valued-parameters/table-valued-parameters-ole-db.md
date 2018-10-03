---
title: 資料表值參數 (OLE DB) |Microsoft Docs
description: 資料表值參數 (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, table-valued parameters
- table-valued parameters (OLE DB)
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 6aa80999bcd7e4633aee7ae0a6aef30838896df6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47628006"
---
# <a name="table-valued-parameters-ole-db"></a>資料表值參數 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  本章節描述 SQL Server 的 OLE DB 驅動程式中的資料表值參數的支援。 其他概觀資訊，請參閱[Parameters &#40;OLE DB Driver for SQL Server&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md)。 如需範例，請參閱[使用資料表值參數&#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)。  
  
## <a name="remarks"></a>Remarks  
 目前可以藉由參數集將多列資料當做程序的參數傳送給伺服器 (**ICommand::Execute** 中的 DBPARAMS 參數)。 使用參數集時，該集合中的每個元素都必須以對伺服器的個別遠端程序呼叫 (RPC) 要求來進行傳送。 資料表值參數提供類似的功能，但能與伺服器更緊密地整合。 如此可以減少 RPC 要求數目，並以集合為基礎在伺服器上進行作業。  
  
 OLE DB 驅動程式支援資料表值參數與 OLE DB 的 SQL server**資料列集**物件。 任何 **Rowset** 物件都可以藉由取用者 (也就是使用 OLE DB Driver for SQL Server 的用戶端應用程式)，以資料表值參數的參數預留位置來提供。 資料表值參數會被視為類似於其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 參數類型。 OLE DB Driver for SQL Server 提供建立、 探索、 規格、 繫結，以及結構描述的介面。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [建立資料表值參數資料列集](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)  
  
-   [資料表值參數類型探索](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-type-discovery.md)  
  
-   [執行包含資料表值參數的命令](../../oledb/ole-db-table-valued-parameters/executing-commands-containing-table-valued-parameters.md)  
  
-   [將資料插入至資料表值參數](../../oledb/ole-db-table-valued-parameters/inserting-data-into-table-valued-parameters.md)  
  
-   [針對 OLE DB 資料表值參數而變更的結構描述資料列集](../../oledb/ole-db-table-valued-parameters/schema-rowsets-changed-for-ole-db-table-valued-parameters.md)  
  
-   [OLE DB 資料表值參數類型支援](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)  
  
-   [OLE DB 資料表值參數類型支援 &#40;方法&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md)  
  
-   [OLE DB 資料表值參數類型支援 &#40;屬性&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md)  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 程式設計](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)   
 [使用資料表值參數 &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
