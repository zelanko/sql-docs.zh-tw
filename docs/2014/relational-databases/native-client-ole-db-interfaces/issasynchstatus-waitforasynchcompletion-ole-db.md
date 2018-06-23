---
title: 'Issasynchstatus:: Waitforasynchcompletion (OLE DB) |Microsoft 文件'
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- WaitForAsynchCompletion method
ms.assetid: 9f65e9e7-eb93-47a1-bc42-acd4649fbd0e
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5c8b2bf4b7ffbc3a478dc872a32053799b6419b6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133491"
---
# <a name="issasynchstatuswaitforasynchcompletion-ole-db"></a>ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
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
 資料列集是在未使用的狀態，因為**itransaction:: Commit**或**itransaction:: Abort**已呼叫或資料列集已取消在其初始化階段。  
  
 DB_E_CANCELED  
 非同步處理已在資料列集擴展或資料來源物件初始化期間取消。  
  
 DB_S_ASYNCHRONOUS  
 即使已經達到指定的逾時，此作業還是尚未完成。  
  
> [!NOTE]  
>  除了上面所列的傳回碼值**issasynchstatus:: Waitforasynchcompletion**方法也支援核心 OLEDB 所傳回的傳回碼值**icommand:: Execute**和**Idbinitialize:: Initialize**方法。  
  
## <a name="remarks"></a>備註  
 **Issasynchstatus:: Waitforasynchcompletion**超過指定的逾時值 （以毫秒為單位），或暫止作業完成之前，不會傳回方法。 **命令**物件具有**CommandTimeout**控制的秒數的內容查詢執行逾時之前。**CommandTimeout**如果搭配使用，將會忽略屬性**issasynchstatus:: Waitforasynchcompletion**方法。  
  
 非同步作業會忽略逾時屬性。 逾時參數**issasynchstatus:: Waitforasynchcompletion**指定會將控制權傳回給呼叫端前經過的時間的最大數量。 如果這個逾時過期，會傳回 DB_S_ASYNCHRONOUS。 逾時絕不會取消非同步作業。 如果應用程式需要取消沒有在逾時期間內完成的非同步作業，它必須等到逾時，然後明確地取消此作業 (如果有傳回 DB_S_ASYNCHRONOUS)。  
  
> [!NOTE]  
>  當使用 OLE DB 服務元件時，可能會傳回 S_OK 時預期 DB_S_ASYNCHRONOUS，讓應用程式應該呼叫[issasynchstatus:: Getstatus](issasynchstatus-getstatus-ole-db.md)檢查傳回 S_OK 或 DB_S_ASYNCHRONOUS 時完成。  
  
 如果*dwMillisecTimeOut*值設定為 INFINITE， **issasynchstatus:: Waitforasynchcompletion**方法會封鎖直到作業完成為止。 如果*dwMillisecTimeOut*值設定為 0，則該方法會立即傳回暫止作業的狀態。 如果逾時在作業完成前過期，將會傳回 DB_S_ASYNCHRONOUS。  
  
 如果作業在逾時過期前完成，傳回的 HRESULT 將會是此作業所傳回的 HRESULT (已經傳回的 HRESULT 已經讓此作業以同步方式執行)。  
  
 此外，SSPROP_ISSAsynchStatus 屬性已加入到 DBPROPSET_SQLSERVERROWSET 屬性集。 支援的提供者[ISSAsynchStatus](issasynchstatus-ole-db.md)介面必須實作這個屬性值為 VARIANT_TRUE。  
  
## <a name="see-also"></a>另請參閱  
 [執行非同步作業](../native-client/features/performing-asynchronous-operations.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](issasynchstatus-ole-db.md)  
  
  