---
title: 執行非同步作業 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
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
caps.latest.revision: 45
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3649167d51f86e8540bc21cc5d932d9203b98369
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131948"
---
# <a name="performing-asynchronous-operations"></a>執行非同步作業
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 允許應用程式執行非同步資料庫作業。 非同步處理可讓方法立即執行，而不會在呼叫的執行緒上封鎖。 這樣可允許多執行緒的許多功能與彈性，而不需要開發人員明確建立執行緒或處理同步。 當初始化資料庫連接或初始化執行命令的結果時，應用程式會要求非同步處理。  
  
## <a name="opening-and-closing-a-database-connection"></a>開啟及關閉資料庫連接  
 當使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者，專門設計來以非同步方式初始化資料來源物件的應用程式可以設定 DBPROPVAL_ASYNCH_INITIALIZE 位元之前呼叫前，於 DBPROP_INIT_ASYNCH 屬性中**Idbinitialize:: Initialize**。 當設定這個屬性時，提供者會立即傳回呼叫**初始化**S_OK 時，如果作業已經立即完成或 DB_S_ASYNCHRONOUS，如果初始設定，以非同步方式繼續執行。 應用程式可以查詢**IDBAsynchStatus**或[ISSAsynchStatus](../../native-client-ole-db-interfaces/issasynchstatus-ole-db.md)資料來源物件上的介面，然後呼叫**idbasynchstatus:: Getstatus**或[Issasynchstatus:: Waitforasynchcompletion](../../native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)取得初始化的狀態。  
  
 此外，SSPROP_ISSAsynchStatus 屬性已加入到 DBPROPSET_SQLSERVERROWSET 屬性集。 支援的提供者**ISSAsynchStatus**介面必須實作這個屬性值為 VARIANT_TRUE。  
  
 **IDBAsynchStatus::Abort**或[issasynchstatus:: Abort](../../native-client-ole-db-interfaces/issasynchstatus-abort-ole-db.md)可以取消非同步呼叫**初始化**呼叫。 取用者必須明確地要求非同步資料來源初始化。 否則， **idbinitialize:: Initialize**不會傳回資料來源物件完全初始化之前。  
  
> [!NOTE]  
>  用於連接共用的資料來源物件不能呼叫**ISSAsynchStatus**介面中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者。 **ISSAsynchStatus**之共用的資料來源物件未公開介面。  
>   
>  如果應用程式明確地強制資料指標引擎，使用**iopenrowset:: Openrowset**和**imultipleresults:: Getresult**將不支援非同步處理。  
>   
>  此外，遠端 proxy/stub dll （在 MDAC 2.8) 無法呼叫**ISSAsynchStatus**介面中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端。 **ISSAsynchStatus**介面不會透過遠端公開。  
>   
>  服務元件不支援**ISSAsynchStatus**。  
  
## <a name="execution-and-rowset-initialization"></a>執行和資料列集初始化  
 設計為非同步開啟執行命令結果的應用程式可以在 DBPROP_ROWSET_ASYNCH 屬性中設定 DBPROPVAL_ASYNCH_INITIALIZE 位元。 當設定此位元，然後才呼叫**idbinitialize:: Initialize**， **icommand:: Execute**， **iopenrowset:: Openrowset**或**IMultipleResults::GetResult**、 *riid*引數必須設定為 IID_IDBAsynchStatus、 IID_ISSAsynchStatus 或 IID_IUnknown。  
  
 方法會立即傳回 S_OK 與如果資料列集初始化立即，則會使用 DB_S_ASYNCHRONOUS 時完成資料列集也會繼續以非同步方式初始化與*ppRowset*上設定要求的介面資料列集。 如[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者，此介面只能是**IDBAsynchStatus**或**ISSAsynchStatus**。 直到資料列集完全初始化時，此介面的行為就好像在暫停的狀態，並呼叫**QueryInterface**以外的介面**IID_IDBAsynchStatus**或**IID_ISSAsynchStatus**可能會傳回 E_NOINTERFACE。 除非取用者明確地要求非同步處理，否則資料列集會以同步的方式進行初始化。 所有要求的介面時，就使用**idbasynchstaus:: Getstatus**或**issasynchstatus:: Waitforasynchcompletion**傳回非同步作業已完成的指示。 這不一定表示資料列集已完全擴展，但是該資料列集是完整的，而且完全可以運作。  
  
 如果在執行的命令不會傳回一個資料列集，它仍會立即傳回的物件來支援**IDBAsynchStatus**。  
  
 如果您需要從非同步命令執行取得多個結果，您應該：  
  
-   在執行命令之前，設定 DBPROP_ROWSET_ASYNCH 屬性的 DBPROPVAL_ASYNCH_INITIALIZE 位元。  
  
-   呼叫**icommand:: Execute**，並要求**IMultipleResults**。  
  
 **IDBAsynchStatus**和**ISSAsynchStatus**介面然後就可以取得透過查詢多個結果介面使用**QueryInterface**。  
  
 當命令完成時執行， **IMultipleResults**可用來當做一般，從同步案例有一個例外狀況： 傳回 DB_S_ASYNCHRONOUS，在此情況下**IDBAsynchStatus**或**ISSAsynchStatus**可用來判斷作業何時完成。  
  
## <a name="examples"></a>範例  
 在下列範例中，應用程式會呼叫非封鎖的方法、進行其他某些處理，然後返回處理結果。 **Issasynchstatus:: Waitforasynchcompletion**等候內部事件物件，直到非同步執行的作業完成或指定的時間量*dwMilisecTimeOut*傳遞。  
  
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
  
 **Issasynchstatus:: Waitforasynchcompletion**等候內部事件物件上以非同步方式執行的作業完成或*dwMilisecTimeOut*值傳遞。  
  
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
 [SQL Server Native Client 功能](sql-server-native-client-features.md)   
 [資料列集屬性和行為](../../native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](../../native-client-ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  