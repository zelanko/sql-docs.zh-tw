---
title: 'Issabort:: Abort (OLE DB) |Microsoft 文件'
ms.custom: ''
ms.date: 03/14/2017
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
- ISSAbort::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
ms.assetid: a5bca169-694b-4895-84ac-e8fba491e479
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 293bc899e2e2c38396b77d1b625895b3b40385f7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  取消目前的資料列集加上與目前命令相關聯之任何批次處理的命令。  
  
**ISSAbort**介面中公開[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者，提供**issabort:: Abort**方法用來取消目前的資料列集加上任何命令批次命令一開始會產生資料列集，並可對尚未完成執行。  
  
 **ISSAbort**是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 提供者特定介面，可以使用**QueryInterface**上**IMultipleResults**所傳回物件**icommand:: Execute**或**iopenrowset:: Openrowset**。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>備註  
 如果要中止的命令位於預存程序中，預存程序 (以及已經呼叫該程序的任何程序) 以及包含預存程序呼叫之命令批次的執行將會結束。 如果伺服器正在將結果集傳送到用戶端，將會停止這個動作。 如果用戶端不想使用結果集，則呼叫**issabort:: Abort**釋放資料列集將會加速資料列集的版本中，但如果沒有開啟的交易，而且 XACT_ABORT 為 ON，將會回復交易之前時**issabort:: Abort**稱為  
  
 之後**issabort:: Abort**傳回 S_OK 時，相關聯**IMultipleResults**介面進入無法使用的狀態並將 db_e_canceled 傳回到所有方法呼叫 (除了所定義的方法**IUnknown**介面) 直到釋放它為止。 如果**IRowset**有取自**IMultipleResults**之前呼叫**中止**，它也會進入無法使用的狀態並將 db_e_canceled 傳回到所有方法呼叫 (除了所定義的方法**IUnknown**介面和**irowset:: Releaserows**) 直到成功呼叫之後釋放它為止**issabort:: Abort**。  
  
> [!NOTE]  
>  開頭為[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，如果伺服器 XACT_ABORT 狀態上，執行**issabort:: Abort**會終止並回復任何目前隱含或明確的交易時連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將不會中止目前的交易。  
  
## <a name="arguments"></a>引數  
 無。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 **Issabort:: Abort**方法會傳回 S_OK，如果已取消批次和 DB_E_CANTCANCEL 否則。 如果批次已經遭到取消，就會傳回 DB_E_CANCELED。  
  
 DB_E_CANCELED  
 批次已經遭到取消。  
  
 DB_E_CANTCANCEL  
 批次未取消。  
  
 E_FAIL  
 發生提供者特定錯誤。詳細資訊，請使用[ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)介面。  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 比方說，物件處於廢止狀態因為**issabort:: Abort**已經呼叫過。  
  
 E_OUTOFMEMORY  
 記憶體不足的錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [ISSAbort & #40; OLE DB & #41;](http://msdn.microsoft.com/library/7c4df482-4a83-4da0-802b-3637b507693a)  
  
  
