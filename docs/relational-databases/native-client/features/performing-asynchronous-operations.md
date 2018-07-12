---
title: 執行非同步作業 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d3bd1ee2baf56a92068d58fffd783cd492609c71
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37420487"
---
# <a name="performing-asynchronous-operations"></a>執行非同步作業
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 允許應用程式執行非同步資料庫作業。 非同步處理可讓方法立即執行，而不會在呼叫的執行緒上封鎖。 這樣可允許多執行緒的許多功能與彈性，而不需要開發人員明確建立執行緒或處理同步。 當初始化資料庫連接或初始化執行命令的結果時，應用程式會要求非同步處理。  
  
## <a name="opening-and-closing-a-database-connection"></a>開啟及關閉資料庫連接  
 使用時[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者，專門設計來以非同步方式初始化資料來源物件的應用程式可以設定 DBPROPVAL_ASYNCH_INITIALIZE 位元呼叫前，於 DBPROP_INIT_ASYNCH 屬性中**Idbinitialize:: Initialize**。 當設定這個屬性時，提供者會立即傳回呼叫**初始化**s_ok 時，如果作業已經立即完成或 DB_S_ASYNCHRONOUS，如果以非同步方式繼續進行初始化。 應用程式可以查詢**IDBAsynchStatus**或是[ISSAsynchStatus](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)介面上的資料來源物件，然後再呼叫**idbasynchstatus:: Getstatus**或[Issasynchstatus:: Waitforasynchcompletion](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)來取得初始化的狀態。  
  
 此外，SSPROP_ISSAsynchStatus 屬性已加入到 DBPROPSET_SQLSERVERROWSET 屬性集。 支援的提供者**ISSAsynchStatus**介面必須實作此屬性值為 VARIANT_TRUE。  
  
 **Idbasynchstatus:: Abort**或是[issasynchstatus:: Abort](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-abort-ole-db.md)可以取消非同步呼叫**初始化**呼叫。 取用者必須明確地要求非同步資料來源初始化。 否則，請**idbinitialize:: Initialize**前不會傳回資料來源物件完全初始化。  
  
> [!NOTE]  
>  用於連接共用的資料來源物件不能呼叫**ISSAsynchStatus**介面中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者。 **ISSAsynchStatus**介面不會公開為集區的資料來源物件。  
>   
>  如果應用程式明確強制使用資料指標引擎，則**iopenrowset:: Openrowset**並**imultipleresults:: Getresult**將不支援非同步處理。  
>   
>  此外，無法呼叫 （在 MDAC 2.8 中) 的遠端 proxy/stub dll **ISSAsynchStatus**介面中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端。 **ISSAsynchStatus**介面不會透過遠端公開。  
>   
>  不支援服務元件**ISSAsynchStatus**。  
  
## <a name="execution-and-rowset-initialization"></a>執行和資料列集初始化  
 設計為非同步開啟執行命令結果的應用程式可以在 DBPROP_ROWSET_ASYNCH 屬性中設定 DBPROPVAL_ASYNCH_INITIALIZE 位元。 當設定此位元，才能呼叫**idbinitialize:: Initialize**， **icommand:: Execute**， **iopenrowset:: Openrowset**或**IMultipleResults::GetResult**，則*riid*引數必須設定為 IID_IDBAsynchStatus、 IID_ISSAsynchStatus 或 IID_IUnknown。  
  
 方法會立即傳回並 S_OK 如果資料列集初始化立即，則會使用 DB_S_ASYNCHRONOUS 時完成的資料列集可讓您繼續以非同步方式初始化與*Pprowset&lt*上設定為要求的介面資料列集。 針對[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者，此介面只能**IDBAsynchStatus**或是**ISSAsynchStatus**。 直到資料列集會完全初始化，此介面的行為，就好像在暫停的狀態，並呼叫**QueryInterface**以外的介面**IID_IDBAsynchStatus**或**IID_ISSAsynchStatus**可能會傳回 E_NOINTERFACE。 除非取用者明確地要求非同步處理，否則資料列集會以同步的方式進行初始化。 所有要求的介面時，就使用**idbasynchstaus:: Getstatus**或是**issasynchstatus:: Waitforasynchcompletion**傳回非同步作業已完成的指示。 這不一定表示資料列集已完全擴展，但是該資料列集是完整的，而且完全可以運作。  
  
 如果執行的命令不會傳回一個資料列集，它仍會立即傳回的物件來支援**IDBAsynchStatus**。  
  
 如果您需要從非同步命令執行取得多個結果，您應該：  
  
-   在執行命令之前，設定 DBPROP_ROWSET_ASYNCH 屬性的 DBPROPVAL_ASYNCH_INITIALIZE 位元。  
  
-   呼叫**icommand:: Execute**，並要求**IMultipleResults**。  
  
 **IDBAsynchStatus**並**ISSAsynchStatus**介面，可再由查詢多個結果介面 using **QueryInterface**。  
  
 當命令完成執行時， **IMultipleResults**可用來當做一般，有一個例外狀況，從同步的情況下： 可能會傳回 DB_S_ASYNCHRONOUS，在此情況下**IDBAsynchStatus**或**ISSAsynchStatus**可用來判斷作業何時完成。  
  
## <a name="examples"></a>範例  
 在下列範例中，應用程式會呼叫非封鎖的方法、進行其他某些處理，然後返回處理結果。 **Issasynchstatus:: Waitforasynchcompletion**等候內部事件物件，直到非同步執行的作業完成或所指定的時間長度*dwMilisecTimeOut*傳遞。  
  
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
  
 **Issasynchstatus:: Waitforasynchcompletion**等候內部事件物件上以非同步方式執行的作業完成或有*dwMilisecTimeOut*值傳遞。  
  
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
  
  
