---
description: 'SQL Server Native Client (OLE DB 中的資料表值參數) '
title: '原生用戶端 OLE DB 提供者 (的資料表值參數) '
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
ms.openlocfilehash: 6e13837ce1d00ae9ea7c113cb64aa9c068a12400
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499041"
---
# <a name="table-valued-parameters--in-sql-server-native-client-ole-db"></a>SQL Server Native Client (OLE DB 中的資料表值參數) 
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  本章節描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者對資料表值參數的支援。 如需其他總覽資訊，請參閱 [&#40;SQL Server Native Client&#41;的資料表值參數 ](../../relational-databases/native-client/features/table-valued-parameters-sql-server-native-client.md)。 如需範例，請參閱[使用資料表值參數 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)。  
  
## <a name="remarks"></a>備註  
 目前可以藉由參數集將多列資料當做程序的參數傳送給伺服器 (**ICommand::Execute** 中的 DBPARAMS 參數)。 使用參數集時，該集合中的每個元素都必須以對伺服器的個別遠端程序呼叫 (RPC) 要求來進行傳送。 資料表值參數提供類似的功能，但能與伺服器更緊密地整合。 如此可以減少 RPC 要求數目，並以集合為基礎在伺服器上進行作業。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 OLE DB 提供者 OLE DB 資料列**集**物件支援資料表值參數。 取用者可以提供任何資料列 **集** 物件 (亦即，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者的用戶端應用程式) 做為資料表值參數參數的預留位置。 資料表值參數會被視為類似於其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 參數類型。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者能提供建立、探索、規格、繫結和結構描述介面。  
  
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
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [使用資料表值參數 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
