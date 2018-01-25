---
title: "擷取單一資料列使用 irow 來 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- SQL Server Native Client OLE DB provider, fetching
ms.assetid: 07c803ca-299a-42c5-ba02-360b9631d15f
caps.latest.revision: "31"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b92878a8f847063e2a2bf18ee6bdaa6433de3d8b
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2018
---
# <a name="fetching-a-single-row-with-irow"></a>使用 IRow 來提取單一資料列
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **IRow**介面中的實作[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者已經過簡化，以提升效能。 **IRow**允許直接存取單一資料列物件的資料行。 如果您事先知道命令執行的結果將會產生一個資料列， **IRow**會擷取該資料列的資料行。 如果結果集包含多個資料列， **IRow**會公開 （expose) 的第一個資料列。  
  
 **IRow**實作不允許資料列的任何瀏覽。 此資料列中的每個資料行只會存取一次，但有一項例外狀況：您可以存取一次資料行來尋找資料行大小，然後再次存取，以便提取資料。  
  
> [!NOTE]  
>  **Irow:: Open**僅支援開啟 DBGUID_STREAM 和 DBGUID_NULL 類型的物件。  
  
 若要取得資料列的物件使用**icommand:: Execute**方法，您必須傳遞 IID_IRow。 **IMultipleResults**介面必須用來處理多個結果集。 **IMultipleResults**支援**IRow**和**IRowset**。 **IRowset**適用於大量作業。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [使用 IRow::GetColumns](../../relational-databases/native-client-ole-db-rowsets/using-irow-getcolumns.md)  
  
-   [使用 IRow 提取 BLOB 資料](http://msdn.microsoft.com/library/badbd6ac-20aa-4891-a14f-48d38e7f30de)  
  
## <a name="see-also"></a>另請參閱  
 [資料列集](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
