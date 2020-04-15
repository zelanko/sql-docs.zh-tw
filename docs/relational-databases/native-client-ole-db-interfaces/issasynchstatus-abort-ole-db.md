---
title: ISSAsynchStatus::Abort (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSAsynchStatus::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
ms.assetid: 2a4bd312-839a-45a8-a299-fc8609be9a2a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 976a23e84492ac9f062ea8d20bcc46545c391e5a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303914"
---
# <a name="issasynchstatusabort-ole-db"></a>ISSAsynchStatus::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  取消非同步執行的作業。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT Abort(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation);  
```  
  
## <a name="arguments"></a>引數  
 *hChapter*[in]  
 要中止作業之章節的控制代碼。 如果被調用的物件不是行集物件,或者操作不適用於章節,則調用方必須將*hCa*設置為DB_NULL_HCHAPTER。  
  
 *eOperation*[in]  
 要中止的作業。 這應該為下列值：  
  
 DBASYNCHOP_OPEN：取消的要求適用於非同步開啟或擴展資料列集，或是非同步初始化資料來源物件。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 已經處理取消非同步作業的要求。 這不保證作業本身已被取消。 若要判斷此作業是否已被取消，取用者應該呼叫 [ISSAsynchStatus::GetStatus](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-getstatus-ole-db.md) 並檢查是否有 DB_E_CANCELED；但是，下一次呼叫時可能不會傳回它。  
  
 DB_E_CANTCANCEL  
 無法取消非同步作業。  
  
 DB_E_CANCELED  
 已經在通知期間取消中止非同步作業的要求。 此作業仍然以非同步的方式執行。  
  
 E_FAIL  
 發生了提供者特定的錯誤。  
  
 E_INVALIDARG  
 *h章*參數不是DB_NULL_HCHAPTER,或者*電子操作*不DBASYNCH_OPEN。  
  
 E_UNEXPECTED  
 **ISSAsynchStatus:abort**是在**IDB 初始化**的數據源物件上調用的:初始化尚未調用或尚未完成。  
  
 **ISSAsynchStatus::Abort**是在**IDB 初始化的**數據源物件上調用的:初始化已調用,但隨後在初始化之前被取消,或者超時。數據源物件仍未初始化。  
  
 **ISSAsynchStatus::Abort**是在**I事務::提交**或**I事務::中止**之前調用的行集中調用的,並且行集在提交或中止中無法存活,並且處於殭屍狀態。  
  
 已在資料列集上呼叫 **ISSAsynchStatus::Abort**，這個資料列集已在其初始化階段非同步地取消。 此資料列集處於廢止狀態。  
  
## <a name="remarks"></a>備註  
 中止資料列集或資料來源物件的初始化可能會讓該資料列集或資料來源物件處於廢止狀態，因此造成 **IUnknown** 方法以外的所有方法都會傳回 E_UNEXPECTED。 當發生這個情況時，取用者唯一可行的動作就是釋放此資料列集或資料來源物件。  
  
 呼叫 **ISSAsynchStatus::Abort** 並針對 *eOperation* 傳回 DBASYNCHOP_OPEN 以外的值將會傳回 S_OK。 這不表示此作業已被取消或完成。  
  
## <a name="see-also"></a>另請參閱  
 [執行非同步作業](../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
  
  
