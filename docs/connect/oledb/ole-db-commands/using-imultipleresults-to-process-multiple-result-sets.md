---
title: 使用 IMultipleResults 來處理多個結果集 |Microsoft 文件
description: 使用 IMultipleResults 來處理多個結果集
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-commands
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- IMultipleResults interface
- multiple-rowset results
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 59e39d472be21161d27b0449c1f2e81d31a09c4d
ms.sourcegitcommit: e1bc8c486680e6d6929c0f5885d97d013a537149
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2018
ms.locfileid: "35666278"
---
# <a name="using-imultipleresults-to-process-multiple-result-sets"></a>使用 IMultipleResults 來處理多個結果集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  取用者會使用**IMultipleResults**介面來處理 OLE DB 驅動程式所傳回的 SQL Server 命令執行的結果。 SQL Server OLE DB 驅動程式提交的命令執行、 當[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行陳述式並傳回任何結果。  
  
 用戶端必須處理命令執行所產生的所有結果。 因為 SQL Server 命令執行 OLE DB 驅動程式可以產生多個資料列集物件當做結果，請使用**IMultipleResults**介面，以確保應用程式資料擷取會完成用戶端起始的往返。  
  
 下列[!INCLUDE[tsql](../../../includes/tsql-md.md)]陳述式會產生多個資料列集，某些包含的資料列資料，從**OrderDetails**資料表和某些包含 COMPUTE BY 子句結果：  
  
```  
SELECT OrderID, FullPrice = (UnitPrice * Quantity), Discount,  
    Discounted = UnitPrice * (1 - Discount) * Quantity  
FROM OrderDetails  
ORDER BY OrderID  
COMPUTE  
    SUM(UnitPrice * Quantity), SUM(UnitPrice * (1 - Discount) * Quantity)  
    BY OrderID  
```  
  
 如果取用者執行包含此文字的命令，並要求資料列集做為傳回的結果介面，則只會傳回第一組資料列。 取用者可能會處理傳回之資料列集中的所有資料列。 但是，如果 DBPROP_MULTIPLECONNECTIONS 資料來源屬性設定為 VARIANT_FALSE，而且會不啟用 MARS 的連接上，沒有其他命令可以 （SQL Server OLE DB 驅動程式將不會建立另一個連接） 的工作階段物件上執行，直到取消命令為止。 如果在連接上未啟用 MARS 時，SQL Server OLE DB 驅動程式會傳回 DB_E_OBJECTOPEN 錯誤，如果 DBPROP_MULTIPLECONNECTIONS 為 VARIANT_FALSE，而且如果沒有使用中交易時，傳回 E_FAIL。  
  
 SQL Server OLE DB 驅動程式也會傳回 db_e_objectopen，而當使用資料流輸出參數和應用程式，尚未取用所有傳回的輸出參數值然後再呼叫**imultipleresults:: Getresults**至取得下一個結果集。 如果沒有啟用 MARS，而連接忙線中執行的命令不會產生資料列集，或產生的資料列集，但不是伺服器資料指標中，如果 DBPROP_MULTIPLECONNECTIONS 資料來源屬性設定為 VARIANT_TRUE 時，SQL Server OLE DB 驅動程式會建立其他連接來支援並行的命令物件，除非交易處於作用中的情況下會傳回錯誤。 交易與鎖定是以連接為基礎，由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理。 如果產生另一個連接，個別連接上的命令不會共用鎖定。 請務必藉由保留另一個命令要求之資料列上的鎖定來確保命令之間不會互相封鎖。 如果有啟用 MARS，在連接上可以有多個命令處於作用中狀態，而如果有使用明確交易，則所有命令都會共用一個公用交易。  
  
 取用者可以使用取消命令[issabort:: Abort](../../oledb/ole-db-interfaces/issabort-abort-ole-db.md)或釋出命令物件和衍生的資料列集上保留的所有參考。  
  
 使用**IMultipleResults**所有執行個體中可讓取用者取得命令執行所產生的所有資料列集，並可讓取用者適當的方式決定取消命令執行，並釋放以供工作階段物件其他命令。  
  
> [!NOTE]  
>  當您使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料指標時，命令執行會建立資料指標。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會傳回資料指標建立成功或失敗，因此，在從命令執行傳回時，會完成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的往返。 每個**GetNextRows**呼叫就會變成往返。 以此種方式，系統可以存在多個作用中的命令物件，而且每個都處理一個屬於伺服器資料指標之提取結果的資料列集。 如需詳細資訊，請參閱[資料列集和 SQL Server 資料指標](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md)。  
  
## <a name="see-also"></a>另請參閱  
 [命令](../../oledb/ole-db-commands/commands.md)  
  
  
