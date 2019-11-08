---
title: 使用 IMultipleResults 來處理多個結果集 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- IMultipleResults interface
- multiple-rowset results
ms.assetid: 754d3f30-7d94-4b67-8dac-baf2699ce9c6
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 52bf85ba17630cc9bd76865e759a55d9c4864afc
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73758224"
---
# <a name="using-imultipleresults-to-process-multiple-result-sets"></a>使用 IMultipleResults 來處理多個結果集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  取用者會使用**IMultipleResults**介面來處理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者命令執行所傳回的結果。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者提交要執行的命令時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會執行語句並傳回任何結果。  
  
 用戶端必須處理命令執行所產生的所有結果。 由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者命令執行可以產生多個資料列集物件當做結果，因此請使用**IMultipleResults**介面，以確保應用程式資料的抓取會完成用戶端起始的來回行程。  
  
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式會產生多個資料列集，其中一些包含來自 **OrderDetails** 資料表的資料列資料，另一些包含 COMPUTE BY 子句的結果：  
  
```  
SELECT OrderID, FullPrice = (UnitPrice * Quantity), Discount,  
    Discounted = UnitPrice * (1 - Discount) * Quantity  
FROM OrderDetails  
ORDER BY OrderID  
COMPUTE  
    SUM(UnitPrice * Quantity), SUM(UnitPrice * (1 - Discount) * Quantity)  
    BY OrderID  
```  
  
 如果取用者執行包含此文字的命令，並要求資料列集做為傳回的結果介面，則只會傳回第一組資料列。 取用者可能會處理傳回之資料列集中的所有資料列。 但是，如果 [DBPROP_MULTIPLECONNECTIONS 資料來源] 屬性設定為 [VARIANT_FALSE]，而且連接上沒有啟用 MARS，則會話物件上不能執行其他命令（[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者將不會建立其他連接）直到取消命令為止。 如果沒有在連接上啟用 MARS，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會在 DBPROP_MULTIPLECONNECTIONS 為 VARIANT_FALSE 時傳回 DB_E_OBJECTOPEN 錯誤，如果有使用中的交易，則傳回 E_FAIL。  
  
 使用資料流程輸出參數時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者也會傳回 DB_E_OBJECTOPEN，而且應用程式在呼叫**IMultipleResults：： GetResults**以取得下一個結果集。 如果未啟用 MARS，而連接忙著執行的命令不會產生資料列集，或產生非伺服器資料指標的資料列集，且 DBPROP_MULTIPLECONNECTIONS 資料來源屬性設定為 VARIANT_TRUE，除非交易正在作用中 (在此情況下會傳回錯誤)，否則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會建立其他連接來支援並行的命令物件。 交易與鎖定是以連接為基礎，由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理。 如果產生另一個連接，個別連接上的命令不會共用鎖定。 請務必藉由保留另一個命令要求之資料列上的鎖定來確保命令之間不會互相封鎖。 如果有啟用 MARS，在連接上可以有多個命令處於作用中狀態，而如果有使用明確交易，則所有命令都會共用一個公用交易。  
  
 取用者可以使用 [ISSAbort::Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)，或釋放保留在命令物件和衍生之資料列集上的所有參考，藉以取消命令。  
  
 在所有執行個體中使用 **IMultipleResults** 可讓取用者取得命令執行所產生的所有資料列集，並讓取用者以適當的方式決定何時取消命令執行，以及釋放工作階段物件供其他命令使用。  
  
> [!NOTE]  
>  當您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料指標時，命令執行會建立資料指標。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回資料指標建立成功或失敗，因此，在從命令執行傳回時，會完成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的往返。 接著，每個 **GetNextRows** 呼叫都會變成往返。 以此種方式，系統可以存在多個作用中的命令物件，而且每個都處理一個屬於伺服器資料指標之提取結果的資料列集。 如需詳細資訊，請參閱[資料列集和 SQL Server 資料指標](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md)。  
  
## <a name="see-also"></a>另請參閱  
 [命令](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
