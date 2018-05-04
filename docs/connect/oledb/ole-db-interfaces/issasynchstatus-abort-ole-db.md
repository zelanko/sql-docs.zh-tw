---
title: 'Issasynchstatus:: Abort (OLE DB) |Microsoft 文件'
description: ISSAsynchStatus::Abort (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAsynchStatus::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 09f95f302ba7ee61fa35d7930d4a783ee43194fb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="issasynchstatusabort-ole-db"></a>ISSAsynchStatus::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  取消非同步執行的作業。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT Abort(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation);  
```  
  
## <a name="arguments"></a>引數  
 *hChapter*[in]  
 要中止作業之章節的控制代碼。 如果所呼叫的物件不是資料列集物件或作業不適用於章節，呼叫端必須將*hChapter*為 DB_NULL_HCHAPTER。  
  
 *eOperation*[in]  
 要中止的作業。 要使用下列值：  
  
 DBASYNCHOP_OPEN：取消的要求適用於非同步開啟或擴展資料列集，或是非同步初始化資料來源物件。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 已經處理取消非同步作業的要求。 它並不保證作業本身已取消。 若要判斷是否已取消作業，取用者應該呼叫[issasynchstatus:: Getstatus](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)並檢查是否有 DB_E_CANCELED; 但是，它可能不會傳回非常下一個呼叫。  
  
 DB_E_CANTCANCEL  
 無法取消非同步作業。  
  
 DB_E_CANCELED  
 已經在通知期間取消中止非同步作業的要求。 此作業仍然以非同步的方式執行。  
  
 E_FAIL  
 發生了提供者特定的錯誤。  
  
 E_INVALIDARG  
 *HChapter*參數不是 DB_NULL_HCHAPTER 或*eOperation*不是 DBASYNCH_OPEN。  
  
 E_UNEXPECTED  
 **Issasynchstatus:: Abort**上的資料來源物件上呼叫**idbinitialize:: Initialize**尚未被呼叫，或尚未完成。  
  
 **Issasynchstatus:: Abort**上的資料來源物件上呼叫**idbinitialize:: Initialize**後續取消之前初始化，但呼叫，或已逾時。此資料來源物件仍未初始化。  
  
 **Issasynchstatus:: Abort**所在的資料列集上呼叫**itransaction:: Commit**或**itransaction:: Abort**之前已呼叫，而且資料列集沒有未被認可或中止，且處於廢止狀態。  
  
 **Issasynchstatus:: Abort**已非同步地取消其初始化階段中的資料列集上呼叫。 此資料列集處於廢止狀態。  
  
## <a name="remarks"></a>備註  
 中止資料列集或資料來源物件的初始化可能會使保留的資料列集或資料來源物件處於廢止狀態，使得以外的所有方法**IUnknown**方法會傳回 E_UNEXPECTED。 當發生這個情況時，取用者唯一可行的動作就是釋放此資料列集或資料來源物件。  
  
 呼叫**issasynchstatus:: Abort**傳遞的值和*eOperation*以外 DBASYNCHOP_OPEN 傳回 S_OK。 這並不代表作業已完成，或已取消。  
  
## <a name="see-also"></a>另請參閱  
 [執行非同步作業](../../oledb/features/performing-asynchronous-operations.md)  
  
  
