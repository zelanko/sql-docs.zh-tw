---
title: 'Issasynchstatus:: Waitforasynchcompletion (OLE DB) |Microsoft 文件'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
apitype: COM
helpviewer_keywords:
- WaitForAsynchCompletion method
ms.assetid: 9f65e9e7-eb93-47a1-bc42-acd4649fbd0e
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0ab8eec0f1eabc796a4acac57abd0af86d8c1982
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32949033"
---
# <a name="issasynchstatuswaitforasynchcompletion-ole-db"></a>ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

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
>  除了上面所列的傳回碼值**issasynchstatus:: Waitforasynchcompletion**方法也支援核心 OLEDB 所傳回的傳回碼值**icommand:: Execute**和**idbinitialize:: Initialize**方法。  
  
## <a name="remarks"></a>備註  
 **Issasynchstatus:: Waitforasynchcompletion**超過指定的逾時值 （以毫秒為單位），或暫止作業完成之前，不會傳回方法。 **命令**物件具有**CommandTimeout**控制的秒數的內容查詢執行逾時之前。**CommandTimeout**如果搭配使用，將會忽略屬性**issasynchstatus:: Waitforasynchcompletion**方法。  
  
 非同步作業會忽略逾時屬性。 逾時參數**issasynchstatus:: Waitforasynchcompletion**指定會將控制權傳回給呼叫端前經過的時間的最大數量。 如果這個逾時過期，會傳回 DB_S_ASYNCHRONOUS。 逾時絕不會取消非同步作業。 如果應用程式需要取消沒有在逾時期間內完成的非同步作業，它必須等到逾時，然後明確地取消此作業 (如果有傳回 DB_S_ASYNCHRONOUS)。  
  
> [!NOTE]  
>  當使用 OLE DB 服務元件時，可能會傳回 S_OK 時預期 DB_S_ASYNCHRONOUS，讓應用程式應該呼叫[issasynchstatus:: Getstatus](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)檢查傳回 S_OK 或 DB_S_ASYNCHRONOUS 時完成。  
  
 如果*dwMillisecTimeOut*值設定為 INFINITE， **issasynchstatus:: Waitforasynchcompletion**方法會封鎖直到作業完成為止。 如果*dwMillisecTimeOut*值設定為 0，則該方法會立即傳回暫止作業的狀態。 如果逾時在作業完成前過期，將會傳回 DB_S_ASYNCHRONOUS。  
  
 如果作業在逾時過期前完成，傳回的 HRESULT 將會是此作業所傳回的 HRESULT (已經傳回的 HRESULT 已經讓此作業以同步方式執行)。  
  
 此外，SSPROP_ISSAsynchStatus 屬性已加入到 DBPROPSET_SQLSERVERROWSET 屬性集。 支援的提供者[ISSAsynchStatus](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)介面必須實作這個屬性值為 VARIANT_TRUE。  
  
## <a name="see-also"></a>另請參閱  
 [執行非同步作業](../../relational-databases/native-client/features/performing-asynchronous-operations.md)   
 [ISSAsynchStatus & #40; OLE DB & #41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
