---
title: ISSAsynchStatus (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSAsynchStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSAsynchStatus interface
ms.assetid: c643f09f-9ccc-4d8b-9243-3cde86c2bd46
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f2c6bc2d66be0b89a62b5b1c678a955891cc06c4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306707"
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **ISSAsynchStatus**公開了[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]對 非同步操作的支援。 這是從核心 OLE DB 介面**IDBAsynchStatus**繼承的可選介面。 除了繼承自 **IDBAsynchStatus** 的 **Abort** 和 **GetStatus** 方法之外，**ISSAsynchStatus** 還提供一個新方法，用來等到非同步作業完成或發生逾時。  
  
|方法|描述|  
|------------|-----------------|  
|[ISSAsynchStatus::Abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-abort-ole-db.md)|取消非同步執行的作業。|  
|[ISSAsynchStatus::GetStatus &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)|傳回以非同步方式執行作業的狀態。|  
|[ISSAsynchStatus::WaitForAsynchCompletion &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)|等到非同步執行的作業完成或發生逾時為止。|  
  
## <a name="remarks"></a>備註  
 **ISSAsynchStatus::GetStatus** 方法的 **ISSAsynchStatus** 實作與 **IDBAsynchStatus::GetStatus** 方法相同，不同的是如果中止資料來源物件的初始化，便會傳回 E_UNEXPECTED，而不是 DB_E_CANCELED (雖然 **ISSAsynchStatus::WaitForAsynchCompletion** 會傳回 DB_E_CANCELED)。 這是因為資料來源物件在中止作業後不會保留在一般的狀態，如此可以讓系統嘗試進一步的初始化作業。  
  
 下列方法支援在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中使用非同步執行：  
  
-   **ICommand::Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>另請參閱  
 [&#40;OLE DB&#41;的接口](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [執行非同步作業](../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
  
  
