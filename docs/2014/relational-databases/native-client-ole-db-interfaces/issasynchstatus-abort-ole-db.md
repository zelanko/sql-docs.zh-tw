---
title: 'Issasynchstatus:: Abort (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ISSAsynchStatus::Abort (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- Abort method
ms.assetid: 2a4bd312-839a-45a8-a299-fc8609be9a2a
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5711cdcdcedb409330ae1b70591d9fe08db961e1
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37414149"
---
# <a name="issasynchstatusabort-ole-db"></a>ISSAsynchStatus::Abort (OLE DB)
  取消非同步執行的作業。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT Abort(  
  HCHAPTER hChapter,  
  DBASYNCHOP eOperation);  
```  
  
## <a name="arguments"></a>引數  
 *hChapter*[in]  
 要中止作業之章節的控制代碼。 如果所呼叫的物件不是資料列集物件或者作業不適用於章節，呼叫端必須將*hChapter*為 DB_NULL_HCHAPTER。  
  
 *eOperation*[in]  
 要中止的作業。 這應該為下列值：  
  
 DBASYNCHOP_OPEN：取消的要求適用於非同步開啟或擴展資料列集，或是非同步初始化資料來源物件。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 已經處理取消非同步作業的要求。 這不保證作業本身已被取消。 若要判斷是否已取消作業，取用者應該呼叫[issasynchstatus:: Getstatus](issasynchstatus-getstatus-ole-db.md)並檢查是否有 DB_E_CANCELED; 但是，它可能不會傳回非常下一個呼叫。  
  
 DB_E_CANTCANCEL  
 無法取消非同步作業。  
  
 DB_E_CANCELED  
 已經在通知期間取消中止非同步作業的要求。 此作業仍然以非同步的方式執行。  
  
 E_FAIL  
 發生了提供者特定的錯誤。  
  
 E_INVALIDARG  
 *HChapter*參數不是 DB_NULL_HCHAPTER 或*eOperation*不是 DBASYNCH_OPEN。  
  
 E_UNEXPECTED  
 **Issasynchstatus:: Abort**上的資料來源物件上呼叫**idbinitialize:: Initialize**尚未呼叫，或尚未完成。  
  
 **Issasynchstatus:: Abort**上的資料來源物件上呼叫**idbinitialize:: Initialize**已呼叫，但後來取消之前的初始化，或已逾時。此資料來源物件仍未初始化。  
  
 **Issasynchstatus:: Abort**所在的資料列集上呼叫**itransaction:: Commit**或**itransaction:: Abort**先前已呼叫，以及資料列集未存留在認可或中止，且在廢止狀態。  
  
 **Issasynchstatus:: Abort**在其初始化階段已非同步地取消資料列集上呼叫。 此資料列集處於廢止狀態。  
  
## <a name="remarks"></a>備註  
 中止資料列集或資料來源物件的初始化可能會讓資料列集或資料來源物件處於廢止狀態，使得以外的所有方法**IUnknown**方法會傳回 E_UNEXPECTED。 當發生這個情況時，取用者唯一可行的動作就是釋放此資料列集或資料來源物件。  
  
 呼叫**issasynchstatus:: Abort**傳遞的值並*eOperation*以外 DBASYNCHOP_OPEN 傳回 S_OK。 這不表示此作業已被取消或完成。  
  
## <a name="see-also"></a>另請參閱  
 [執行非同步作業](../native-client/features/performing-asynchronous-operations.md)  
  
  
