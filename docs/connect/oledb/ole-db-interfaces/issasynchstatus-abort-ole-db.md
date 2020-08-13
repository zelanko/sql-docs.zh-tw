---
title: ISSAsynchStatus::Abort (OLE DB 驅動程式) | Microsoft Docs
description: ISSAsynchStatus::Abort (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSAsynchStatus::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: e3c6e3ba45774362834c8a8391f5658670e01434
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87244331"
---
# <a name="issasynchstatusabort-ole-db"></a>ISSAsynchStatus::Abort (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  取消非同步執行的作業。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT Abort(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation);  
```  
  
## <a name="arguments"></a>引數  
 *hChapter*[in]  
 要中止作業之章節的控制代碼。 如果所呼叫的物件不是資料列集物件或是此作業不適用於章節，呼叫端必須將 *hChapter* 設定為 DB_NULL_HCHAPTER。  
  
 *eOperation*[in]  
 要中止的作業。 應使用下列值：  
  
 DBASYNCHOP_OPEN：取消的要求適用於非同步開啟或擴展資料列集，或是非同步初始化資料來源物件。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 已經處理取消非同步作業的要求。 這不保證作業本身已被取消。 若要判斷此作業是否已被取消，取用者應該呼叫 [ISSAsynchStatus::GetStatus](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md) 並檢查是否有 DB_E_CANCELED；但是，下一次呼叫時可能不會傳回它。  
  
 DB_E_CANTCANCEL  
 無法取消非同步作業。  
  
 DB_E_CANCELED  
 已經在通知期間取消中止非同步作業的要求。 此作業仍然以非同步的方式執行。  
  
 E_FAIL  
 發生了提供者特定的錯誤。  
  
 E_INVALIDARG  
 *hChapter* 參數不是 DB_NULL_HCHAPTER 或 *eOperation* 不是 DBASYNCH_OPEN。  
  
 E_UNEXPECTED  
 已在尚未呼叫或完成 **IDBInitialize::Initialize** 的資料來源物件上呼叫 **ISSAsynchStatus::Abort**。  
  
 已在呼叫 **IDBInitialize::Initialize** 的資料來源物件上呼叫 **ISSAsynchStatus::Abort**，但是接著在初始化之前將它取消，或是它已經逾時。此資料來源物件仍未初始化。  
  
 在之前已呼叫 **ITransaction::Commit** 或 **ITransaction::Abort** 的資料列集上呼叫 **ISSAsynchStatus::Abort**，而且此資料列集並未在認可或中止時存活下來，因此處於廢止狀態。  
  
 已在資料列集上呼叫 **ISSAsynchStatus::Abort**，這個資料列集已在其初始化階段非同步地取消。 此資料列集處於廢止狀態。  
  
## <a name="remarks"></a>備註  
 中止資料列集或資料來源物件的初始化可能會讓該資料列集或資料來源物件處於廢止狀態，因此造成 **IUnknown** 方法以外的所有方法都會傳回 E_UNEXPECTED。 當發生這個情況時，取用者唯一可行的動作就是釋放此資料列集或資料來源物件。  
  
 呼叫 **ISSAsynchStatus::Abort** 並針對 *eOperation* 傳回 DBASYNCHOP_OPEN 以外的值將會傳回 S_OK。 這不表示此作業已被取消或完成。  
  
## <a name="see-also"></a>另請參閱  
 [執行非同步作業](../../oledb/features/performing-asynchronous-operations.md)  
  
  
