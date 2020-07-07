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
ms.openlocfilehash: eb263a1b61f7da765eff38d9b10eba683e8d86d2
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86005385"
---
# <a name="issasynchstatusabort-ole-db"></a>ISSAsynchStatus::Abort (OLE DB)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  取消非同步執行的作業。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT Abort(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation);  
```  
  
## <a name="arguments"></a>引數  
 *hChapter*[in]  
 要中止作業之章節的控制代碼。 如果所呼叫的物件不是資料列集物件，或作業不適用於某個章節，則呼叫端必須將*hchapter 設定*設定為 DB_Null_HCHAPTER。  
  
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
 *Hchapter 設定*參數不 DB_Null_HCHAPTER，或*eOperation*不 DBASYNCH_OPEN。  
  
 E_UNEXPECTED  
 在尚未呼叫**IDBInitialize：： Initialize**的資料來源物件上呼叫**ISSAsynchStatus：： Abort** ，或尚未完成。  
  
 在呼叫了**IDBInitialize：： Initialize**的資料來源物件上呼叫了**ISSAsynchStatus：： Abort** ，但後來在初始化之前取消，或已超時。資料來源物件仍未初始化。  
  
 在先前呼叫了**ITransaction：： Commit**或**ITransaction：： abort**的資料列集上呼叫**ISSAsynchStatus：： Abort** ，而且資料列集不會存留在 Commit 或 Abort，而且處於廢止狀態。  
  
 已在資料列集上呼叫 **ISSAsynchStatus::Abort**，這個資料列集已在其初始化階段非同步地取消。 此資料列集處於廢止狀態。  
  
## <a name="remarks"></a>備註  
 中止資料列集或資料來源物件的初始化可能會讓該資料列集或資料來源物件處於廢止狀態，因此造成 **IUnknown** 方法以外的所有方法都會傳回 E_UNEXPECTED。 當發生這個情況時，取用者唯一可行的動作就是釋放此資料列集或資料來源物件。  
  
 呼叫 **ISSAsynchStatus::Abort** 並針對 *eOperation* 傳回 DBASYNCHOP_OPEN 以外的值將會傳回 S_OK。 這不表示此作業已被取消或完成。  
  
## <a name="see-also"></a>另請參閱  
 [執行非同步作業](../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
  
  
