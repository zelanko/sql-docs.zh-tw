---
title: I多倍結果,多個結果集
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c5e19cef4e00fc1c55e29e51ccea13c2fdb7a0e2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304441"
---
# <a name="using-imultipleresults-to-process-multiple-result-sets"></a>使用 IMultipleResults 來處理多個結果集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  消費者使用**IMulti 結果**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]介面來處理 本機用戶端 OLE DB 提供程式命令執行返回的結果。 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式提交執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]命令時, 執行語句並返回任何結果。  
  
 用戶端必須處理命令執行所產生的所有結果。 由於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式提供程式命令執行可以生成多個行集物件作為結果,因此使用**IMulti 結果**介面確保應用程式數據檢索完成用戶端啟動的往返。  
  
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式會產生多個資料列集，其中一些包含來自 **OrderDetails** 資料表的資料列資料，另一些包含 COMPUTE BY 子句的結果：  
  
```sql
SELECT OrderID, FullPrice = (UnitPrice * Quantity), Discount,  
    Discounted = UnitPrice * (1 - Discount) * Quantity  
FROM OrderDetails  
ORDER BY OrderID  
COMPUTE  
    SUM(UnitPrice * Quantity), SUM(UnitPrice * (1 - Discount) * Quantity)  
    BY OrderID  
```  
  
 如果取用者執行包含此文字的命令，並要求資料列集做為傳回的結果介面，則只會傳回第一組資料列。 取用者可能會處理傳回之資料列集中的所有資料列。 但是,如果DBPROP_MULTIPLECONNECTIONS資料來源屬性設置為VARIANT_FALSE,並且未在連接上啟用 MARS,則在取消命令之前,無法在工作階段物件上執行其他命令[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]( 本機用戶端 OLE 資料庫提供者不會創建其他連接)。 如果在連接上未啟用 MARS,則[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果 DBPROP_MULTIPLECONNECTIONSVARIANT_FALSE,則本機用戶端 OLE DB 提供程式將返回DB_E_OBJECTOPEN錯誤,如果存在活動事務,則返回E_FAIL。  
  
 使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]流式輸出參數時,本機用戶端 OLE DB 提供程式也將返回DB_E_OBJECTOPEN,並且應用程式在調用**IMultiResult::getResult**獲取下一個結果集之前,未使用所有返回的輸出參數值。 如果未啟用 MARS，而連接忙著執行的命令不會產生資料列集，或產生非伺服器資料指標的資料列集，且 DBPROP_MULTIPLECONNECTIONS 資料來源屬性設定為 VARIANT_TRUE，除非交易正在作用中 (在此情況下會傳回錯誤)，否則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會建立其他連接來支援並行的命令物件。 交易與鎖定是以連接為基礎，由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理。 如果產生另一個連接，個別連接上的命令不會共用鎖定。 請務必藉由保留另一個命令要求之資料列上的鎖定來確保命令之間不會互相封鎖。 如果有啟用 MARS，在連接上可以有多個命令處於作用中狀態，而如果有使用明確交易，則所有命令都會共用一個公用交易。  
  
 取用者可以使用 [ISSAbort::Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)，或釋放保留在命令物件和衍生之資料列集上的所有參考，藉以取消命令。  
  
 在所有執行個體中使用 **IMultipleResults** 可讓取用者取得命令執行所產生的所有資料列集，並讓取用者以適當的方式決定何時取消命令執行，以及釋放工作階段物件供其他命令使用。  
  
> [!NOTE]  
>  當您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料指標時，命令執行會建立資料指標。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回資料指標建立成功或失敗，因此，在從命令執行傳回時，會完成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的往返。 接著，每個 **GetNextRows** 呼叫都會變成往返。 以此種方式，系統可以存在多個作用中的命令物件，而且每個都處理一個屬於伺服器資料指標之提取結果的資料列集。 如需詳細資訊，請參閱[資料列集和 SQL Server 資料指標](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md)。  
  
## <a name="see-also"></a>另請參閱  
 [命令](../../relational-databases/native-client-ole-db-commands/commands.md)  
  
  
