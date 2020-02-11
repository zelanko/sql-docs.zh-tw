---
title: ADO 事件模型範例（VC + +） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Visual C++ code examples [ADO], event model
ms.assetid: 29530153-b963-4a7c-8665-2335f1d604a8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1af45d9ac4674af98097083e2da89a217f17a58f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67921019"
---
# <a name="ado-events-model-example-vc"></a>ADO 事件模型範例 (VC++)
Ado 事件具現[化（依語言](../../../ado/guide/data/ado-event-instantiation-by-language.md)）的 Visual C++ 區段會提供如何具現化 ado 事件模型的一般描述。 以下是在 **#import**指示詞所建立的環境中，具現化事件模型的特定範例。  
  
 一般描述會使用**adoint**做為方法簽章的參考。 不過，一般描述中的一些詳細資料會因使用 **#import**指示詞而稍微變更：  
  
-   **#Import**指示詞會解析其基本形式的**typedef**、方法簽章資料類型和修飾詞。  
  
-   必須覆寫的純虛擬方法，其前面都會加上 "**raw_**"。  
  
 有些程式碼只會反映編碼樣式。  
  
-   **建議**方法所使用的**IUnknown**指標是透過呼叫**QueryInterface**來明確取得。  
  
-   您不需要在類別定義中明確地撰寫函式的程式碼。  
  
-   您可能想要撰寫更健全的 QueryInterface、AddRef 和 Release 的程式碼。  
  
-   **__Uuidof （）** 指示詞會廣泛用來取得介面識別碼。  
  
 最後，此範例包含一些工作程式碼。  
  
-   此範例會撰寫為主控台應用程式。  
  
-   您應該在批註 "`// Do some work`" 底下插入自己的程式碼。  
  
-   所有事件處理常式都預設為不執行任何動作，並取消進一步的通知。 您應該為應用程式插入適當的程式碼，並在必要時允許通知。  
  
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
