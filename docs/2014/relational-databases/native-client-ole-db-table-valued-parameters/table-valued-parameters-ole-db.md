---
title: 資料表值參數 (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, table-valued parameters
- table-valued parameters (OLE DB)
ms.assetid: 4298b73d-615b-4d28-9843-03b4d5fc489e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9c58b1837eb017a3cc51652ff404b37690b3849
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046424"
---
# <a name="table-valued-parameters-ole-db"></a>資料表值參數 (OLE DB)
  本章節描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者對資料表值參數的支援。 其他概觀資訊，請參閱[Parameters &#40;SQL Server Native Client&#41;](../native-client/features/table-valued-parameters-sql-server-native-client.md)。 如需範例，請參閱[使用資料表值參數&#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)。  
  
## <a name="remarks"></a>備註  
 目前可以藉由參數集將多個資料列當做程序的參數傳送給伺服器 (`ICommand::Execute` 中的 DBPARAMS 參數)。 使用參數集時，該集合中的每個元素都必須以對伺服器的個別遠端程序呼叫 (RPC) 要求來進行傳送。 資料表值參數提供類似的功能，但能與伺服器更緊密地整合。 如此可以減少 RPC 要求數目，並以集合為基礎在伺服器上進行作業。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者中，是以 OLE DB `Rowset` 物件的形式支援資料表值參數。 任何 `Rowset` 物件都可以藉由取用者 (也就是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者的用戶端應用程式)，以資料表值參數的參數預留位置來提供。 資料表值參數會被視為類似於其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 參數類型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者能提供建立、探索、規格、繫結和結構描述介面。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [建立資料表值參數資料列集](table-valued-parameter-rowset-creation.md)  
  
-   [資料表值參數類型探索](../../database-engine/dev-guide/table-valued-parameter-type-discovery.md)  
  
-   [執行包含資料表值參數的命令](executing-commands-containing-table-valued-parameters.md)  
  
-   [將資料插入至資料表值參數](inserting-data-into-table-valued-parameters.md)  
  
-   [針對 OLE DB 資料表值參數而變更的結構描述資料列集](schema-rowsets-changed-for-ole-db-table-valued-parameters.md)  
  
-   [OLE DB 資料表值參數類型支援](ole-db-table-valued-parameter-type-support.md)  
  
-   [OLE DB 資料表值參數類型支援 &#40;方法&#41;](ole-db-table-valued-parameter-type-support-methods.md)  
  
-   [OLE DB 資料表值參數類型支援 &#40;屬性&#41;](ole-db-table-valued-parameter-type-support-properties.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)   
 [使用資料表值參數 &#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
