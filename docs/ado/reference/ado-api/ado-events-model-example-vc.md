---
title: ADO 事件模型範例 （VC + +） |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Visual C++ code examples [ADO], event model
ms.assetid: 29530153-b963-4a7c-8665-2335f1d604a8
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 20df675bbbee8b513f7e1008da0cb4772255701c
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35275467"
---
# <a name="ado-events-model-example-vc"></a>ADO 事件模型範例 （VC + +）
Visual c + + 部分[ADO 事件具現化語言](../../../ado/guide/data/ado-event-instantiation-by-language.md)如何具現化 ADO 事件模型的一般說明。 以下是具現化所建立的環境內的事件模型的特定範例 **#import**指示詞。  
  
 使用的一般描述**adoint.h**方法簽章的參考。 不過，少數的詳細資料中的一般描述變更稍微使用 **#import**指示詞：  
  
-   **#Import**指示詞解析**typedef**的方法簽章資料類型和修飾詞，以其基本形式。  
  
-   必須覆寫的純虛擬方法都會所有加上"**raw_**"。  
  
 部分程式碼只會反映程式碼撰寫樣式。  
  
-   將指標**IUnknown**使用**Advise**方法呼叫會明確地取得**QueryInterface**。  
  
-   您不需要明確的程式碼中的類別定義解構函式。  
  
-   您可以在程式碼更強固的 QueryInterface、 AddRef 及發行的實作。  
  
-   **__Uuidof()** 指示詞會廣泛地用來取得介面識別碼。  
  
 最後，此範例包含一些運作的程式碼。  
  
-   此範例會寫入成為主控台應用程式。  
  
-   您應該插入您自己的程式碼在註解中，「`// Do some work`"。  
  
-   所有的事件處理常式預設不進行任何動作，並取消進一步通知。 您應該將適當的程式碼插入您的應用程式，並視需要允許通知。  
  
```  
// ADO_Events_Model_Example.cpp  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
// The Connection events  
class CConnEvent : public ConnectionEventsVt {  
private:  
   ULONG m_cRef;  
  
public:  
   CConnEvent() { m_cRef = 0; };  
   ~CConnEvent() {};  
  
   STDMETHODIMP QueryInterface(REFIID riid, void ** ppv);  
   STDMETHODIMP_(ULONG) AddRef();  
   STDMETHODIMP_(ULONG) Release();  
  
   STDMETHODIMP raw_InfoMessage( struct Error *pError,   
                                 EventStatusEnum *adStatus,   
                                 struct _Connection *pConnection);  
  
   STDMETHODIMP raw_BeginTransComplete( LONG TransactionLevel,  
                                        struct Error *pError,  
                                        EventStatusEnum *adStatus,  
                                        struct _Connection *pConnection);  
  
   STDMETHODIMP raw_CommitTransComplete( struct Error *pError,   
                                         EventStatusEnum *adStatus,  
                                         struct _Connection *pConnection);  
  
   STDMETHODIMP raw_RollbackTransComplete( struct Error *pError,   
                                           EventStatusEnum *adStatus,  
                                           struct _Connection *pConnection);  
  
   STDMETHODIMP raw_WillExecute( BSTR *Source,  
                                 CursorTypeEnum *CursorType,  
                                 LockTypeEnum *LockType,  
                                 long *Options,  
                                 EventStatusEnum *adStatus,  
                                 struct _Command *pCommand,  
                                 struct _Recordset *pRecordset,  
                                 struct _Connection *pConnection);  
  
   STDMETHODIMP raw_ExecuteComplete( LONG RecordsAffected,  
                                     struct Error *pError,  
                                     EventStatusEnum *adStatus,  
                                     struct _Command *pCommand,  
                                     struct _Recordset *pRecordset,  
                                     struct _Connection *pConnection);  
  
   STDMETHODIMP raw_WillConnect( BSTR *ConnectionString,  
                                 BSTR *UserID,  
                                 BSTR *Password,  
                                 long *Options,  
                                 EventStatusEnum *adStatus,  
                                 struct _Connection *pConnection);  
  
   STDMETHODIMP raw_ConnectComplete( struct Error *pError,  
                                     EventStatusEnum *adStatus,  
                                     struct _Connection *pConnection);  
  
   STDMETHODIMP raw_Disconnect( EventStatusEnum *adStatus, struct _Connection *pConnection);  
};  
  
// The Recordset events  
class CRstEvent : public RecordsetEventsVt {  
private:  
   ULONG m_cRef;     
  
public:  
   CRstEvent() { m_cRef = 0; };  
   ~CRstEvent() {};  
  
   STDMETHODIMP QueryInterface(REFIID riid, void ** ppv);  
   STDMETHODIMP_(ULONG) AddRef();  
   STDMETHODIMP_(ULONG) Release();  
  
   STDMETHODIMP raw_WillChangeField( LONG cFields,        
                                     VARIANT Fields,  
                                     EventStatusEnum *adStatus,  
                                     struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_FieldChangeComplete( LONG cFields,  
                                         VARIANT Fields,  
                                         struct Error *pError,  
                                         EventStatusEnum *adStatus,  
                                         struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_WillChangeRecord( EventReasonEnum adReason,  
                                      LONG cRecords,  
                                      EventStatusEnum *adStatus,  
                                      struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_RecordChangeComplete( EventReasonEnum adReason,  
                                          LONG cRecords,  
                                          struct Error *pError,  
                                          EventStatusEnum *adStatus,  
                                          struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_WillChangeRecordset( EventReasonEnum adReason,  
                                         EventStatusEnum *adStatus,  
                                         struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_RecordsetChangeComplete( EventReasonEnum adReason,  
                                             struct Error *pError,  
                                             EventStatusEnum *adStatus,  
                                             struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_WillMove( EventReasonEnum adReason,  
                              EventStatusEnum *adStatus,  
                              struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_MoveComplete( EventReasonEnum adReason,  
                                  struct Error *pError,  
                                  EventStatusEnum *adStatus,  
                                  struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_EndOfRecordset( VARIANT_BOOL *fMoreData,  
                                    EventStatusEnum *adStatus,  
                                    struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_FetchProgress( long Progress,  
                                   long MaxProgress,  
                                   EventStatusEnum *adStatus,  
                                   struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_FetchComplete( struct Error *pError,   
                                   EventStatusEnum *adStatus,  
                                   struct _Recordset *pRecordset);  
};  
  
// Implement each connection method  
STDMETHODIMP CConnEvent::raw_InfoMessage( struct Error *pError,   
                                         EventStatusEnum *adStatus,  
                                         struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_BeginTransComplete( LONG TransactionLevel,  
                                                 struct Error *pError,  
                                                 EventStatusEnum *adStatus,  
                                                 struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_CommitTransComplete( struct Error *pError,  
                                                  EventStatusEnum *adStatus,  
                                                  struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_RollbackTransComplete( struct Error *pError,  
                                                    EventStatusEnum *adStatus,  
                                                    struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_WillExecute( BSTR *Source,  
                                          CursorTypeEnum *CursorType,  
                                          LockTypeEnum *LockType,  
                                          long *Options,  
                                          EventStatusEnum *adStatus,  
                                          struct _Command *pCommand,  
                                          struct _Recordset *pRecordset,  
                                          struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_ExecuteComplete( LONG RecordsAffected,  
                                              struct Error *pError,  
                                              EventStatusEnum *adStatus,  
                                              struct _Command *pCommand,  
                                              struct _Recordset *pRecordset,  
                                              struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_WillConnect( BSTR *ConnectionString,  
                                          BSTR *UserID,  
                                          BSTR *Password,  
                                          long *Options,  
                                          EventStatusEnum *adStatus,  
                                          struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_ConnectComplete( struct Error *pError,  
                                              EventStatusEnum *adStatus,  
                                              struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_Disconnect( EventStatusEnum *adStatus, struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
// Implement each recordset method  
STDMETHODIMP CRstEvent::raw_WillChangeField( LONG cFields,  
                                             VARIANT Fields,  
                                             EventStatusEnum *adStatus,  
                                             struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_FieldChangeComplete( LONG cFields,  
                                                 VARIANT Fields,  
                                                 struct Error *pError,  
                                                 EventStatusEnum *adStatus,  
                                                 struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_WillChangeRecord( EventReasonEnum adReason,  
                                              LONG cRecords,  
                                              EventStatusEnum *adStatus,  
                                              struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_RecordChangeComplete( EventReasonEnum adReason,  
                                                  LONG cRecords,  
                                                  struct Error *pError,  
                                                  EventStatusEnum *adStatus,  
                                                  struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_WillChangeRecordset( EventReasonEnum adReason,  
                                                 EventStatusEnum *adStatus,  
                                                 struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_RecordsetChangeComplete( EventReasonEnum adReason,  
                                                     struct Error *pError,  
                                                     EventStatusEnum *adStatus,  
                                                     struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_WillMove( EventReasonEnum adReason,   
                                      EventStatusEnum *adStatus,  
                                      struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_MoveComplete( EventReasonEnum adReason,  
                                          struct Error *pError,  
                                          EventStatusEnum *adStatus,  
                                          struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_EndOfRecordset( VARIANT_BOOL *fMoreData,  
                                            EventStatusEnum *adStatus,  
                                            struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_FetchProgress( long Progress,  
                                           long MaxProgress,  
                                           EventStatusEnum *adStatus,  
                                           struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_FetchComplete( struct Error *pError,  
                                           EventStatusEnum *adStatus,  
                                           struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::QueryInterface(REFIID riid, void ** ppv) {  
   *ppv = NULL;  
   if (riid == __uuidof(IUnknown) || riid == __uuidof(RecordsetEventsVt))   
      *ppv = this;  
  
   if (*ppv == NULL)  
      return ResultFromScode(E_NOINTERFACE);  
  
   AddRef();  
   return NOERROR;  
}  
  
STDMETHODIMP_(ULONG) CRstEvent::AddRef() {   
   return ++m_cRef;   
};  
  
STDMETHODIMP_(ULONG) CRstEvent::Release() {   
   if (0 != --m_cRef)   
      return m_cRef;  
   delete this;  
   return 0;  
}  
  
STDMETHODIMP CConnEvent::QueryInterface(REFIID riid, void ** ppv) {  
   *ppv = NULL;  
   if (riid == __uuidof(IUnknown) || riid == __uuidof(ConnectionEventsVt))   
      *ppv = this;  
  
   if (*ppv == NULL)  
      return ResultFromScode(E_NOINTERFACE);  
  
   AddRef();  
   return NOERROR;  
}  
  
STDMETHODIMP_(ULONG) CConnEvent::AddRef() {   
   return ++m_cRef;   
};  
  
STDMETHODIMP_(ULONG) CConnEvent::Release() {   
   if (0 != --m_cRef)   
      return m_cRef;  
   delete this;  
   return 0;  
}  
  
int main() {  
   HRESULT hr;  
   DWORD dwConnEvt;  
   DWORD dwRstEvt;  
   IConnectionPointContainer *pCPC = NULL;  
   IConnectionPoint *pCP = NULL;  
   IUnknown *pUnk = NULL;  
   CRstEvent *pRstEvent = NULL;  
   CConnEvent *pConnEvent= NULL;  
   int rc = 0;  
   _RecordsetPtr pRst;   
   _ConnectionPtr pConn;  
  
   ::CoInitialize(NULL);  
  
   hr = pConn.CreateInstance(__uuidof(Connection));  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pRst.CreateInstance(__uuidof(Recordset));  
  
   if (FAILED(hr))   
      return rc;  
  
   // Start using the Connection events  
   hr = pConn->QueryInterface(__uuidof(IConnectionPointContainer), (void **)&pCPC);  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCPC->FindConnectionPoint(__uuidof(ConnectionEvents), &pCP);  
   pCPC->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   pConnEvent = new CConnEvent();  
   hr = pConnEvent->QueryInterface(__uuidof(IUnknown), (void **) &pUnk);  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCP->Advise(pUnk, &dwConnEvt);  
   pCP->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   // Start using the Recordset events  
   hr = pRst->QueryInterface(__uuidof(IConnectionPointContainer), (void **)&pCPC);  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCPC->FindConnectionPoint(__uuidof(RecordsetEvents), &pCP);  
   pCPC->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   pRstEvent = new CRstEvent();  
   hr = pRstEvent->QueryInterface(__uuidof(IUnknown), (void **) &pUnk);  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCP->Advise(pUnk, &dwRstEvt);  
   pCP->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   // Do some work  
   pConn->Open("dsn=DataPubs;", "", "", adConnectUnspecified);  
   pRst->Open("SELECT * FROM authors", (IDispatch *) pConn, adOpenStatic, adLockReadOnly, adCmdText);  
  
   pRst->MoveFirst();  
   while (pRst->EndOfFile == FALSE) {  
      wprintf(L"Name = '%s'\n", (wchar_t*) ((_bstr_t) pRst->Fields->GetItem("au_lname")->Value));  
      pRst->MoveNext();  
   }  
  
   pRst->Close();  
   pConn->Close();  
  
   // Stop using the Connection events  
   hr = pConn->QueryInterface(__uuidof(IConnectionPointContainer), (void **) &pCPC);  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCPC->FindConnectionPoint(__uuidof(ConnectionEvents), &pCP);  
   pCPC->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCP->Unadvise( dwConnEvt );  
   pCP->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   // Stop using the Recordset events  
   hr = pRst->QueryInterface(__uuidof(IConnectionPointContainer), (void **) &pCPC);  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCPC->FindConnectionPoint(__uuidof(RecordsetEvents), &pCP);  
   pCPC->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCP->Unadvise( dwRstEvt );  
   pCP->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   CoUninitialize();  
}  
```
