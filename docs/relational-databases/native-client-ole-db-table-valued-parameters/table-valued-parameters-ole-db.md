---
title: 資料表值參數 (OLE DB) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 15055f582d7add6194753e2743d63b5e082318b5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300226"
---
# <a name="table-valued-parameters-ole-db"></a>資料表值參數 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本章節描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者對資料表值參數的支援。 有關其他概述資訊,請參閱[&#40;SQL 伺服器本機用戶端&#41;的表值參數](../../relational-databases/native-client/features/table-valued-parameters-sql-server-native-client.md)。 如需範例，請參閱[使用資料表值參數 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)。  
  
## <a name="remarks"></a>備註  
 目前可以藉由參數集將多列資料當做程序的參數傳送給伺服器 (**ICommand::Execute** 中的 DBPARAMS 參數)。 使用參數集時，該集合中的每個元素都必須以對伺服器的個別遠端程序呼叫 (RPC) 要求來進行傳送。 資料表值參數提供類似的功能，但能與伺服器更緊密地整合。 如此可以減少 RPC 要求數目，並以集合為基礎在伺服器上進行作業。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式中支援表值參數作為 OLE DB**行集**物件。 任何**Rowset**物件都可以由消費者([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]即使用 本機用戶端 OLE DB 提供程式的用戶端應用程式)作為表值參數的占位符提供。 資料表值參數會被視為類似於其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 參數類型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者能提供建立、探索、規格、繫結和結構描述介面。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [建立資料表值參數資料列集](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)  
  
-   [資料表值參數類型探索](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameter-type-discovery.md)  
  
-   [執行包含表值參數的指令](../../relational-databases/native-client-ole-db-table-valued-parameters/executing-commands-containing-table-valued-parameters.md)  
  
-   [將資料插入至資料表值參數](../../relational-databases/native-client-ole-db-table-valued-parameters/inserting-data-into-table-valued-parameters.md)  
  
-   [為 OLE DB 表值參數變更架構列集](../../relational-databases/native-client-ole-db-table-valued-parameters/schema-rowsets-changed-for-ole-db-table-valued-parameters.md)  
  
-   [OLE DB 資料表值參數類型支援](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)  
  
-   [OLE DB 資料表值參數類型支援 &#40;方法&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md)  
  
-   [OLE DB 資料表值參數類型支援 &#40;屬性&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL 伺服器本機用戶端&#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [使用資料表值參數 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
