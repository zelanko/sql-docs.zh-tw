---
description: '使用 IRow 提取單一資料列 (Native Client OLE DB 提供者) '
title: 使用 IRow 提取單一資料列 (Native Client OLE DB 提供者) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- SQL Server Native Client OLE DB provider, fetching
ms.assetid: 07c803ca-299a-42c5-ba02-360b9631d15f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0e70f3aa9fc0faef9a6c80d5009818329dd7abcc
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868727"
---
# <a name="fetching-a-single-row-with-irow-native-client-ole-db-provider"></a>使用 IRow 提取單一資料列 (Native Client OLE DB 提供者) 
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  **IRow** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生用戶端 OLE DB 提供者中的 IRow 介面可簡化，以提升效能。 **IRow** 允許直接存取單一資料列物件的資料行。 如果您事先知道命令執行的結果只會產生單一資料列，**IRow** 就會擷取該資料列的資料行。 如果結果集包含多個資料列，**IRow** 就只會公開第一個資料列。  
  
 **IRow** 實作不允許資料列的任何導覽。 此資料列中的每個資料行只會存取一次，但有一項例外狀況：您可以存取一次資料行來尋找資料行大小，然後再次存取，以便提取資料。  
  
> [!NOTE]  
>  **IRow::Open** 僅支援開啟 DBGUID_STREAM 和 DBGUID_NULL 類型的物件。  
  
 若要使用 **ICommand::Execute** 方法來取得資料列物件，您必須傳遞 IID_IRow。 **IMultipleResults** 介面必須用來處理多個結果集。 **IMultipleResults** 支援 **IRow** 和 **IRowset**。 **IRowset** 可用於大量作業。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [使用 IRow::GetColumns](../../relational-databases/native-client-ole-db-rowsets/using-irow-getcolumns.md)  
  
-   [使用 IRow 擷取 BLOB 資料]()  
  
## <a name="see-also"></a>另請參閱  
 [資料列集](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
