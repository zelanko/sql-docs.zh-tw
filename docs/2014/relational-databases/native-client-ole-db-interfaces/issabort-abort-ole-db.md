---
title: 'Issabort:: Abort (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSAbort::Abort (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- Abort method
ms.assetid: a5bca169-694b-4895-84ac-e8fba491e479
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8ad1310112b3cd6ac536a55a82757ae99433372d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62511512"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
  取消目前的資料列集加上與目前命令相關聯之任何批次處理的命令。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>備註  
 如果要中止的命令位於預存程序中，預存程序 (以及已經呼叫該程序的任何程序) 以及包含預存程序呼叫之命令批次的執行將會結束。 如果伺服器正在將結果集傳送到用戶端，將會停止這個動作。 如果用戶端不想要取用結果集，在釋放資料列集前呼叫 **ISSAbort::Abort** 將會加速資料列集的釋放，但是如果有開啟的交易，而且 XACT_ABORT 為 ON，呼叫 **ISSAbort::Abort** 時，將會回復交易  
  
 在後**issabort:: Abort**會傳回 s_ok 時，相關聯**IMultipleResults**介面進入無法使用的狀態並將 db_e_canceled 傳回到所有方法呼叫 (除了所定義的方法**IUnknown**介面) 直到釋放它為止。 如果在呼叫 **Abort** 前已經從 **IMultipleResults** 取得 **IRowset**，它也會進入無法使用狀態，並將 DB_E_CANCELED 傳回到所有方法呼叫 (除了 **IUnknown** 介面和 **IRowset::ReleaseRows** 所定義的方法以外)，直到成功呼叫 **ISSAbort::Abort** 後釋放它為止。  
  
> [!NOTE]  
>  從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，如果伺服器 XACT_ABORT 狀態為 ON，執行 **ISSAbort::Abort** 會終止並回復連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的任何目前隱含或明確交易。 舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將不會中止目前的交易。  
  
## <a name="arguments"></a>引數  
 無。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 **ISSAbort::Abort** 方法會傳回 S_OK，如果批次遭到取消，則為 DB_E_CANTCANCEL。 如果批次已經遭到取消，就會傳回 DB_E_CANCELED。  
  
 DB_E_CANCELED  
 批次已經遭到取消。  
  
 DB_E_CANTCANCEL  
 批次未取消。  
  
 E_FAIL  
 發生提供者特有的錯誤;如需詳細資訊，請使用[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)介面。  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 例如，物件會因為已經呼叫 **ISSAbort::Abort** 而處於廢止狀態。  
  
 E_OUTOFMEMORY  
 記憶體不足的錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [ISSAbort &#40;OLE DB&#41;](../../database-engine/dev-guide/issabort-ole-db.md)  
  
  
