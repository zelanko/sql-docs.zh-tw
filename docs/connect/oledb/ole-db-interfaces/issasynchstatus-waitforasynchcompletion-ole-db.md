---
title: 'Issasynchstatus:: Waitforasynchcompletion (OLE DB) |Microsoft Docs'
description: ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
apitype: COM
helpviewer_keywords:
- WaitForAsynchCompletion method
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 6df61043aae6f86ab4c632c58323e4d670cfcd7c
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2018
ms.locfileid: "51030025"
---
# <a name="issasynchstatuswaitforasynchcompletion-ole-db"></a>ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  等到非同步執行的作業完成或發生逾時為止。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT WaitForAsynchCompletion(   
        DWORD dwMillisecTimeOut);  
```  
  
## <a name="arguments"></a>引數  
 *dwMillisecTimeOut*[in]  
 逾時 (以毫秒為單位)。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功。  
  
 E_UNEXPECTED  
 資料列處於未使用狀態，因為在其初始化階段，已經呼叫 **ITransaction::Commit** 或 **ITransaction::Abort**，或者已經取消資料列集。  
  
 DB_E_CANCELED  
 非同步處理已在資料列集擴展或資料來源物件初始化期間取消。  
  
 DB_S_ASYNCHRONOUS  
 即使已經達到指定的逾時，此作業還是尚未完成。  
  
> [!NOTE]  
>  除了以上列出的傳回碼值，**ISSAsynchStatus::WaitForAsynchCompletion** 方法也支援透過核心 OLEDB **ICommand::Execute** 和 **IDBInitialize::Initialize** 方法所傳回的傳回碼值。  
  
## <a name="remarks"></a>Remarks  
 在逾時值 (以毫秒為單位) 已過，或暫止的作業完成前，**ISSAsynchStatus::WaitForAsynchCompletion** 方法將不會傳回。 **Command** 物件的 **CommandTimeout** 屬性會控制查詢在逾時前執行的秒數。如果搭配 **ISSAsynchStatus::WaitForAsynchCompletion** 方法使用，將會忽略 **CommandTimeout** 屬性。  
  
 非同步作業會忽略逾時屬性。 **ISSAsynchStatus::WaitForAsynchCompletion** 的逾時參數會指定將控制項傳回給呼叫端前經過的時間上限。 如果這個逾時過期，會傳回 DB_S_ASYNCHRONOUS。 逾時絕不會取消非同步作業。 如果應用程式需要取消沒有在逾時期間內完成的非同步作業，它必須等到逾時，然後明確地取消此作業 (如果有傳回 DB_S_ASYNCHRONOUS)。  
  
> [!NOTE]  
>  使用 OLE DB 服務元件時，如果為 DB_S_ASYNCHRONOUS，可能會傳回 S_OK；因此，應用程式應該呼叫 [ISSAsynchStatus::GetStatus](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md) 來檢查傳回 S_OK 或 DB_S_ASYNCHRONOUS 時，作業是否完成。  
  
 如果 *dwMillisecTimeOut* 值設定為 INFINITE，**ISSAsynchStatus::WaitForAsynchCompletion** 方法會封鎖，直到作業完成為止。 如果 *dwMillisecTimeOut* 值設定為 0，則方法將會立即傳回暫止之作業的狀態。 如果逾時在作業完成前過期，將會傳回 DB_S_ASYNCHRONOUS。  
  
 如果作業在逾時過期前完成，傳回的 HRESULT 將會是此作業所傳回的 HRESULT (已經傳回的 HRESULT 已經讓此作業以同步方式執行)。  
  
 此外，SSPROP_ISSAsynchStatus 屬性已加入到 DBPROPSET_SQLSERVERROWSET 屬性集。 支援 [ISSAsynchStatus](../../oledb/ole-db-interfaces/issasynchstatus-ole-db.md) 介面的提供者必須使用 VARIANT_TRUE 的值實作此屬性。  
  
## <a name="see-also"></a>另請參閱  
 [執行非同步作業](../../oledb/features/performing-asynchronous-operations.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
