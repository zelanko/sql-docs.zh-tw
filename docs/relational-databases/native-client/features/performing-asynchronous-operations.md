---
title: 執行非同步作業 | Microsoft Docs
description: 允許應用程式使用 SQL Server Native Client 舊 DB 提供者來執行非同步資料庫作業。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- initialization [SQL Server Native Client]
- database connections [SQL Server Native Client]
- data access [SQL Server Native Client], asynchronous operations
- connections [SQL Server Native Client]
- asynchronous operations [SQL Server Native Client]
- rowsets [SQL Server], initializing
- SQLNCLI, asynchronous operations
- SQL Server Native Client, asynchronous operations
ms.assetid: 8fbd84b4-69cb-4708-9f0f-bbdf69029bcc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8008c9e206ea5f9c8459292a2576df6d3d165fef
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247625"
---
# <a name="performing-asynchronous-operations-in-sql-server-native-client"></a>在 SQL Server Native Client 中執行非同步作業
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 允許應用程式執行非同步資料庫作業。 非同步處理可讓方法立即執行，而不會在呼叫的執行緒上封鎖。 這樣可允許多執行緒的許多功能與彈性，而不需要開發人員明確建立執行緒或處理同步。 當初始化資料庫連接或初始化執行命令的結果時，應用程式會要求非同步處理。  
  
## <a name="opening-and-closing-a-database-connection"></a>開啟及關閉資料庫連接  
 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者時，設計為以非同步方式初始化資料來源物件的應用程式，可以在呼叫**IDBInitialize：： initialize**之前，在 DBPROP_INIT_ASYNCH 屬性中設定 DBPROPVAL_ASYNCH_INITIALIZE 位。 設定此屬性時，如果作業已經立即完成，提供者會使用 S_OK 立即從 **Initialize** 的呼叫傳回；如果初始化是以非同步方式繼續，則會使用 DB_S_ASYNCHRONOUS 從此呼叫傳回。 應用程式可以在資料來源物件上查詢**IDBAsynchStatus**或[ISSAsynchStatus](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)介面，然後呼叫**IDBAsynchStatus：： GetStatus**或[ISSAsynchStatus：： WaitForAsynchCompletion](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)來取得初始化的狀態。  
  
 此外，SSPROP_ISSAsynchStatus 屬性已加入到 DBPROPSET_SQLSERVERROWSET 屬性集。 支援 **ISSAsynchStatus** 介面的提供者必須使用 VARIANT_TRUE 的值實作此屬性。  
  
 呼叫 **IDBAsynchStatus::Abort** 或 [ISSAsynchStatus::Abort](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-abort-ole-db.md) 可以取消非同步的 **Initialize** 呼叫。 取用者必須明確地要求非同步資料來源初始化。 否則，要等到資料來源物件完全初始化之後，**IDBInitialize::Initialize** 才會傳回。  
  
> [!NOTE]  
>  用於連接共用的資料來源物件無法在**ISSAsynchStatus** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者中呼叫 ISSAsynchStatus 介面。 **ISSAsynchStatus** 介面不會針對集區資料來源物件公開。  
>   
>  如果應用程式明確地強制使用資料指標引擎，**IOpenRowset::OpenRowset** 和 **IMultipleResults::GetResult** 將不支援非同步處理。  
>   
>  此外，遠端 proxy/stub dll （在 MDAC 2.8 中）無法呼叫 Native Client 中的**ISSAsynchStatus**介面 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 **ISSAsynchStatus** 介面不會透過遠端公開。  
>   
>  服務元件不支援 **ISSAsynchStatus**。  
  
## <a name="execution-and-rowset-initialization"></a>執行和資料列集初始化  
 設計為非同步開啟執行命令結果的應用程式可以在 DBPROP_ROWSET_ASYNCH 屬性中設定 DBPROPVAL_ASYNCH_INITIALIZE 位元。 呼叫 **IDBInitialize::Initialize**、**ICommand::Execute**、**IOpenRowset::OpenRowset** 或 **IMultipleResults::GetResult** 之前設定此位元時，必須將 *riid* 引數設定為 IID_IDBAsynchStatus、IID_ISSAsynchStatus 或 IID_Iunknown。  
  
 如果資料列集初始化立即完成，此方法會使用 S_OK 立即傳回；如果資料列集在 *ppRowset* 設定為資料列集上要求的介面時，繼續以非同步方式初始化，則會使用 DB_S_ASYNCHRONOUS 傳回此方法。 針對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者，此介面只能是**IDBAsynchStatus**或**ISSAsynchStatus**。 在資料列集完全初始化之前，此介面的行為如同處於已暫停狀態，而且針對 **IID_IDBAsynchStatus** 或 **IID_ISSAsynchStatus** 之外的介面呼叫 **QueryInterface** 可能會傳回 E_NOINTERFACE。 除非取用者明確地要求非同步處理，否則資料列集會以同步的方式進行初始化。 如果 **IDBAsynchStaus::GetStatus** 或 **ISSAsynchStatus::WaitForAsynchCompletion** 傳回時，指出非同步作業已完成，則可使用所有要求的介面。 這不一定表示資料列集已完全擴展，但是該資料列集是完整的，而且完全可以運作。  
  
 如果執行的命令並未傳回資料列集，它仍然會使用支援 **IDBAsynchStatus** 的物件立即傳回。  
  
 如果您需要從非同步命令執行取得多個結果，您應該：  
  
-   在執行命令之前，設定 DBPROP_ROWSET_ASYNCH 屬性的 DBPROPVAL_ASYNCH_INITIALIZE 位元。  
  
-   呼叫 **ICommand::Execute**，並要求 **IMultipleResults**。  
  
 接著，使用 **QueryInterface** 來查詢多個結果介面，藉此取得 **IDBAsynchStatus** 和 **ISSAsynchStatus** 介面。  
  
 當命令執行完成時，除非同步案例的一個例外，否則可以如常使用 **IMultipleResults**：可以傳回 DB_S_ASYNCHRONOUS，在此情況下，**IDBAsynchStatus** 或 **ISSAsynchStatus** 可用於判斷作業完成的時間。  
  
## <a name="examples"></a>範例  
 在下列範例中，應用程式會呼叫非封鎖的方法、進行其他某些處理，然後返回處理結果。 **ISSAsynchStatus::WaitForAsynchCompletion** 會等候內部事件物件，直到非同步執行作業完成，或是過了 *dwMilisecTimeOut* 所指定的時間為止。  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
  
DBPROPSET CmdPropset[1];  
DBPROP CmdProperties[1];  
  
CmdPropset[0].rgProperties = CmdProperties;  
CmdPropset[0].cProperties = 1;  
CmdPropset[0].guidPropertySet = DBPROPSET_ROWSET;  
  
// Set asynch mode for command.  
CmdProperties[0].dwPropertyID = DBPROP_ROWSET_ASYNCH;  
CmdProperties[0].vValue.vt = VT_I4;  
CmdProperties[0].vValue.lVal = DBPROPVAL_ASYNCH_INITIALIZE;  
CmdProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
  
hr = pICommandProps->SetProperties(1, CmdPropset);  
  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work here...  
  
   hr = pISSAsynchStatus->WaitForAsynchCompletion(dwMilisecTimeOut);  
   if ( hr == S_OK)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
      pISSAsynchStatus->Release();  
   }  
}  
```  
  
 **ISSAsynchStatus::WaitForAsynchCompletion** 會等候內部事件物件，直到非同步執行作業完成，或是過了 *dwMilisecTimeOut* 值為止。  
  
 下列範例會示範利用多個結果集的非同步處理：  
  
```  
DBPROP CmdProperties[1];  
  
// Set asynch mode for command.  
CmdProperties[0].dwPropertyID = DBPROP_ROWSET_ASYNCH;  
CmdProperties[0].vValue.vt = VT_I4;  
CmdProperties[0].vValue.lVal = DBPROPVAL_ASYNCH_INITIALIZE;  
  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_IMultipleResults,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pIMultipleResults);  
  
// Use GetResults for ISSAsynchStatus.  
hr = pIMultipleResults->GetResult(IID_ISSAsynchStatus, (void **) &pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work here...  
  
   hr = pISSAsynchStatus->WaitForAsynchCompletion(dwMilisecTimeOut);  
   if (hr == S_OK)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
      pISSAsynchStatus->Release();  
   }  
}  
```  
  
 若要防止封鎖，用戶端可以檢查執行中非同步作業的狀態，如下列範例所示：  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);   
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   do{  
      // Do some work...  
      hr = pISSAsynchStatus->GetStatus(DB_NULL_HCHAPTER, DBASYNCHOP_OPEN, NULL, NULL, &ulAsynchPhase, NULL);  
   }while (DBASYNCHPHASE_COMPLETE != ulAsynchPhase)  
   if SUCCEEDED(hr)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
   }  
   pIDBAsynchStatus->Release();  
}  
```  
  
 下列範例會示範如何取消目前執行中的非同步作業：  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work...  
   hr = pISSAsynchStatus->Abort(DB_NULL_HCHAPTER, DBASYNCHOP_OPEN);  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [資料列集屬性和行為](../../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
