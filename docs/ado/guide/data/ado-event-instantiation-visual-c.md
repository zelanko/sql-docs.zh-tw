---
title: ADO 事件具現化： Visual C++ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 385ad90a-37d0-497c-94aa-935d21fed78f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a839ffc977981c977c2675f25dae4d505e89b081
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926050"
---
# <a name="ado-event-instantiation-visual-c"></a>ADO 事件具現化：Visual C++
這是如何在 Microsoft® Visual C++®中將 ADO 事件具現化的描述。 如需完整的說明，請參閱[ADO 事件模型範例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md) 。  
  
 建立衍生自**ConnectionEventsVt**和**RecordsetEventsVt**介面（從檔案 adoint 中找到）的類別。  
  
```  
// BeginEventExampleVC01  
class CConnEvent : public ConnectionEventsVt  
{  
    public:  
    STDMETHODIMP InfoMessage(   
            ADOError *pError,  
            EventStatusEnum *adStatus,  
            _ADOConnection *pConnection);  
...  
}  
  
class CRstEvent : public RecordsetEventsVt   
{  
    public:  
        STDMETHODIMP WillChangeField(   
                LONG cFields,  
                VARIANT Fields,  
                EventStatusEnum *adStatus,  
                _ADORecordset *pRecordset);  
...  
}  
// EndEventExampleVC01  
```  
  
 在這兩個類別中，執行每個事件處理常式方法。 每個方法都已足夠只傳回 S_OK 的 HRESULT。 不過，當您讓它知道您的事件處理常式可以使用時，預設會連續呼叫它們。 相反地，您可能會想要在第一次將**adStatus**設定為**adStatusUnwantedEvent**之後，不要求進一步通知。  
  
```  
// BeginEventExampleVC02  
STDMETHODIMP CConnEvent::ConnectComplete(  
            ADOError *pError,  
            EventStatusEnum *adStatus,  
            _ADOConnection *pConnection)   
        {  
        *adStatus = adStatusUnwantedEvent;  
        return S_OK;  
        }  
  
// EndEventExampleVC02  
```  
  
 事件類別繼承自**IUnknown**，因此您也必須執行**QueryInterface**、 **AddRef**和**Release**方法。 也會執行類別的函式和析構函式。 選擇您最熟悉的 Visual C++ 工具來簡化這部分的工作。  
  
 藉由在**IConnectionPointContainer**和**IConnectionPoint**介面的[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)和[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件上發出**QueryInterface** ，讓它知道您的事件處理常式可供使用。 然後針對每個類別發出**IConnectionPoint：： Advise** 。  
  
 例如，假設您使用布耳函數，如果它成功通知**記錄集**物件您有可用的事件處理常式，則會傳回**True** 。  
  
```  
// BeginEventExampleVC03  
HRESULT    hr;  
DWORD      dwEvtClass;  
IConnectionPointContainer    *pCPC = NULL;  
IConnectionPoint             *pCP = NULL;  
CRstEvent                    *pRStEvent = NULL;  
...  
_RecordsetPtr                pRs;  
pRs.CreateInstance(__uuidof(Recordset));  
pRStEvent = new CRstEvent;  
if (pRStEvent == NULL) return FALSE;  
...  
hr = pRs->QueryInterface(IID_IConnectionPointContainer, (LPVOID *)&pCPC);  
if (FAILED(hr)) return FALSE;  
hr = pCPC->FindConnectionPoint(RecordsetEvents, &pCP);  
pCPC->Release();    // Always Release now, even before checking.  
if (FAILED(hr)) return FALSE;  
hr = pCP->Advise(pRstEvent, &dwEvtClass);   //Turn on event support.  
pCP->Release();  
if (FAILED(hr)) return FALSE;  
...  
return TRUE;  
...  
// EndEventExampleVC03  
```  
  
 此時，會啟用**RecordsetEvent**系列的事件，並在發生**記錄集**事件時呼叫您的方法。  
  
 之後，當您想要讓事件處理常式無法使用時，請再次取得連接點，併發出**IConnectionPoint：： Unadvise**方法。  
  
```  
// BeginEventExampleVC04  
...  
hr = pCP->Unadvise(dwEvtClass);    //Turn off event support.  
pCP->Release();  
if (FAILED(hr)) return FALSE;  
...  
// EndEventExampleVC04  
```  
  
 您必須適當地發行介面和終結類別物件。  
  
 下列程式碼顯示**記錄集**事件接收類別的完整範例。  
  
```  
// BeginEventExampleVC05.cpp  
// compile with: /LD  
#include <adoint.h>  
  
class CADORecordsetEvents : public RecordsetEventsVt {  
  
public:  
   ULONG m_ulRefCount;  
   CADORecordsetEvents():m_ulRefCount(1){}  
  
   STDMETHOD(QueryInterface)(REFIID iid, LPVOID * ppvObject) {  
      if (IsEqualIID(__uuidof(IUnknown), iid) || IsEqualIID(__uuidof(RecordsetEventsVt), iid)) {  
         *ppvObject = this;  
         return S_OK;  
      }  
      else   
         return E_NOINTERFACE;  
   }  
  
   STDMETHOD_(ULONG, AddRef)() {  
      return m_ulRefCount++;  
   }  
  
   STDMETHOD_(ULONG, Release)() {  
      if (--m_ulRefCount == 0) {  
         delete this;  
         return 0;  
      }  
      else   
         return m_ulRefCount;  
   }  
  
   STDMETHOD(WillChangeField)( LONG cFields,   
                               VARIANT Fields,   
                               EventStatusEnum *adStatus,  
                               _ADORecordset *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
  
   STDMETHOD(FieldChangeComplete)( LONG cFields,  
                                   VARIANT Fields,  
                                   ADOError *pError,  
                                   EventStatusEnum *adStatus,  
                                   _ADORecordset *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
  
   STDMETHOD(WillChangeRecord)( EventReasonEnum adReason,  
                                LONG cRecords,  
                                EventStatusEnum *adStatus,  
                                _ADORecordset *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
  
   STDMETHOD(RecordChangeComplete)( EventReasonEnum adReason,  
                                    LONG cRecords,  
                                    ADOError  *pError,  
                                    EventStatusEnum  *adStatus,  
                                    _ADORecordset  *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
  
   STDMETHOD(WillChangeRecordset)( EventReasonEnum adReason,  
                                   EventStatusEnum *adStatus,  
                                   _ADORecordset  *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
  
   STDMETHOD(RecordsetChangeComplete)( EventReasonEnum adReason,  
                                       ADOError *pError,  
                                       EventStatusEnum  *adStatus,  
                                       _ADORecordset  *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
  
   STDMETHOD(WillMove)( EventReasonEnum adReason,  
                        EventStatusEnum  *adStatus,  
                        _ADORecordset  *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
  
   STDMETHOD(MoveComplete)( EventReasonEnum adReason,  
                            ADOError *pError,  
                            EventStatusEnum *adStatus,  
                            _ADORecordset  *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
  
   STDMETHOD(EndOfRecordset)( VARIANT_BOOL *fMoreData,  
                              EventStatusEnum *adStatus,  
                              _ADORecordset *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
  
   STDMETHOD(FetchProgress)( long Progress,  
                             long MaxProgress,  
                             EventStatusEnum *adStatus,  
                             _ADORecordset *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
  
   STDMETHOD(FetchComplete)( ADOError *pError,  
                             EventStatusEnum *adStatus,  
                             _ADORecordset *pRecordset) {  
      *adStatus = adStatusUnwantedEvent;   
      return S_OK;  
   }  
};  
```
