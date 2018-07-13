---
title: 'Issabort:: Abort (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ISSAbort::Abort (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- Abort method
ms.assetid: a5bca169-694b-4895-84ac-e8fba491e479
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 05673bb90cd0958344a6a12550f15c122489219a
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37416287"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
  取消目前的資料列集加上與目前命令相關聯之任何批次處理的命令。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>備註  
 如果要中止的命令位於預存程序中，預存程序 (以及已經呼叫該程序的任何程序) 以及包含預存程序呼叫之命令批次的執行將會結束。 如果伺服器正在將結果集傳送到用戶端，將會停止這個動作。 如果用戶端不想使用結果集，則呼叫**issabort:: Abort**之前釋放資料列集時，將會加速資料列集的版本中，但是如果沒有開啟的交易，而且 XACT_ABORT 為 ON，則會復原交易時**Issabort:: Abort**稱為  
  
 在後**issabort:: Abort**會傳回 s_ok 時，相關聯**IMultipleResults**介面進入無法使用的狀態並將 db_e_canceled 傳回到所有方法呼叫 (除了所定義的方法**IUnknown**介面) 直到釋放它為止。 如果**IRowset**有取自**IMultipleResults**之前呼叫**中止**，它也會進入無法使用的狀態，並傳回 DB_E_CANCELED 所有方法呼叫 （所定義的方法除了**IUnknown**介面並**irowset:: Releaserows**) 發行之後成功呼叫為止**issabort:: Abort**.  
  
> [!NOTE]  
>  開頭[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，如果伺服器 XACT_ABORT 狀態上，執行**issabort:: Abort**將會終止並回復任何目前隱含或明確的交易時連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將不會中止目前的交易。  
  
## <a name="arguments"></a>引數  
 無。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 **Issabort:: Abort**方法會傳回 S_OK，如果批次已取消 db_e_cantcancel 否則。 如果批次已經遭到取消，就會傳回 DB_E_CANCELED。  
  
 DB_E_CANCELED  
 批次已經遭到取消。  
  
 DB_E_CANTCANCEL  
 批次未取消。  
  
 E_FAIL  
 發生提供者特有的錯誤;如需詳細資訊，請使用[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)介面。  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 比方說，物件是在廢止狀態因為**issabort:: Abort**已經呼叫過。  
  
 E_OUTOFMEMORY  
 記憶體不足的錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [ISSAbort &#40;OLE DB&#41;](../../database-engine/dev-guide/issabort-ole-db.md)  
  
  
