---
title: 資料表值參數（OLE DB） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, table-valued parameters
- table-valued parameters (OLE DB)
ms.assetid: 4298b73d-615b-4d28-9843-03b4d5fc489e
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 67991d5bd50b9612b8f3eaff01d37eef581b22f5
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761643"
---
# <a name="table-valued-parameters-ole-db"></a>資料表值參數 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本章節描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者對資料表值參數的支援。 如需其他總覽資訊，請參閱[資料表值&#40;參數&#41;SQL Server Native Client](../../relational-databases/native-client/features/table-valued-parameters-sql-server-native-client.md)。 如需範例，請參閱[使用資料表值參數&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)。  
  
## <a name="remarks"></a>Remarks  
 目前可以藉由參數集將多列資料當做程序的參數傳送給伺服器 (**ICommand::Execute** 中的 DBPARAMS 參數)。 使用參數集時，該集合中的每個元素都必須以對伺服器的個別遠端程序呼叫 (RPC) 要求來進行傳送。 資料表值參數提供類似的功能，但能與伺服器更緊密地整合。 如此可以減少 RPC 要求數目，並以集合為基礎在伺服器上進行作業。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者中支援資料表值參數，做為 OLE DB 資料列**集**物件。 任何資料列**集**物件都可以由取用者（也就是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者的用戶端應用程式）提供，做為資料表值參數參數的預留位置。 資料表值參數會被視為類似於其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 參數類型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者能提供建立、探索、規格、繫結和結構描述介面。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [建立資料表值參數資料列集](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)  
  
-   [資料表值參數類型探索](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameter-type-discovery.md)  
  
-   [執行包含資料表值參數的命令](../../relational-databases/native-client-ole-db-table-valued-parameters/executing-commands-containing-table-valued-parameters.md)  
  
-   [將資料插入至資料表值參數](../../relational-databases/native-client-ole-db-table-valued-parameters/inserting-data-into-table-valued-parameters.md)  
  
-   [針對 OLE DB 資料表值參數而變更的結構描述資料列集](../../relational-databases/native-client-ole-db-table-valued-parameters/schema-rowsets-changed-for-ole-db-table-valued-parameters.md)  
  
-   [OLE DB 資料表值參數類型支援](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)  
  
-   [OLE DB 資料表值參數類型支援 &#40;方法&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md)  
  
-   [OLE DB 資料表值參數類型支援 &#40;屬性&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;OLE DB&#41; ](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [使用資料表值參數 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
