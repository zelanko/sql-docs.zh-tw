---
title: 使用 IMultipleResults 來處理多個結果集 | Microsoft Docs
description: 使用 IMultipleResults 來處理多個結果集
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- IMultipleResults interface
- multiple-rowset results
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 405acf9e72cac6188c284ef040c4f5b27ac4af7d
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86004924"
---
# <a name="using-imultipleresults-to-process-multiple-result-sets"></a>使用 IMultipleResults 來處理多個結果集
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  取用者會使用 **IMultipleResults** 介面來處理 OLE DB Driver for SQL Server 命令執行所傳回的結果。 當 OLE DB Driver for SQL Server 提交要執行的命令時，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會執行陳述式並傳回任何結果。  
  
 用戶端必須處理命令執行所產生的所有結果。 由於 OLE DB Driver for SQL Server 命令執行可以產生多個資料列集物件當做結果，因此使用 **IMultipleResults** 介面可確保應用程式資料擷取會完成用戶端起始的往返。  
  
 下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式會產生多個資料列集，其中一些包含來自 **OrderDetails** 資料表的資料列資料，另一些包含 COMPUTE BY 子句的結果：  
  
```  
SELECT OrderID, FullPrice = (UnitPrice * Quantity), Discount,  
    Discounted = UnitPrice * (1 - Discount) * Quantity  
FROM OrderDetails  
ORDER BY OrderID  
COMPUTE  
    SUM(UnitPrice * Quantity), SUM(UnitPrice * (1 - Discount) * Quantity)  
    BY OrderID  
```  
  
 如果取用者執行包含此文字的命令，並要求資料列集做為傳回的結果介面，則只會傳回第一組資料列。 取用者可能會處理傳回之資料列集中的所有資料列。 但是，如果 DBPROP_MULTIPLECONNECTIONS 資料來源屬性設定為 VARIANT_FALSE，而且連接上沒有啟用 MARS，則沒有其他命令可以在工作階段物件上執行 (OLE DB Driver for SQL Server 將不會建立其他連接)，直到取消命令為止。 如果沒有在連接上啟用 MARS，OLE DB Driver for SQL Server 會在 DBPROP_MULTIPLECONNECTIONS 為 VARIANT_FALSE 時，傳回 DB_E_OBJECTOPEN 錯誤，並在有作用中的交易時，傳回 E_FAIL。  
  
 使用資料流輸出參數，而且應用程式在呼叫 **IMultipleResults::GetResults** 取得下一個結果集前，尚未取用所有傳回的輸出參數值時，OLE DB Driver for SQL Server 也會傳回 DB_E_OBJECTOPEN。 如果未啟用 MARS，而連接忙著執行的命令不會產生資料列集，或產生非伺服器資料指標的資料列集，且 DBPROP_MULTIPLECONNECTIONS 資料來源屬性設定為 VARIANT_TRUE，除非交易正在作用中 (在此情況下會傳回錯誤)，否則 OLE DB Driver for SQL Server 會建立其他連接來支援並行的命令物件。 交易與鎖定是以連接為基礎，由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理。 如果產生另一個連接，個別連接上的命令不會共用鎖定。 請務必藉由保留另一個命令要求之資料列上的鎖定來確保命令之間不會互相封鎖。 如果有啟用 MARS，在連接上可以有多個命令處於作用中狀態，而如果有使用明確交易，則所有命令都會共用一個公用交易。  
  
 取用者可以使用 [ISSAbort::Abort](../../oledb/ole-db-interfaces/issabort-abort-ole-db.md)，或釋放保留在命令物件和衍生之資料列集上的所有參考，藉以取消命令。  
  
 在所有執行個體中使用 **IMultipleResults** 可讓取用者取得命令執行所產生的所有資料列集，並讓取用者以適當的方式決定何時取消命令執行，以及釋放工作階段物件供其他命令使用。  
  
> [!NOTE]  
>  當您使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料指標時，命令執行會建立資料指標。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會傳回資料指標建立成功或失敗，因此，在從命令執行傳回時，會完成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的往返。 接著，每個 **GetNextRows** 呼叫都會變成往返。 以此種方式，系統可以存在多個作用中的命令物件，而且每個都處理一個屬於伺服器資料指標之提取結果的資料列集。 如需詳細資訊，請參閱[資料列集和 SQL Server 資料指標](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md)。  
  
## <a name="see-also"></a>另請參閱  
 [命令](../../oledb/ole-db-commands/commands.md)  
  
  
