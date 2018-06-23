---
title: 'Issabort:: Abort (OLE DB) |Microsoft 文件'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0729183a2e5be91d3cdb30eae3ae5990f8398103
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131704"
---
# <a name="issabortabort-ole-db"></a>ISSAbort::Abort (OLE DB)
  取消目前的資料列集加上與目前命令相關聯之任何批次處理的命令。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT Abort(void);  
```  
  
## <a name="remarks"></a>備註  
 如果要中止的命令位於預存程序中，預存程序 (以及已經呼叫該程序的任何程序) 以及包含預存程序呼叫之命令批次的執行將會結束。 如果伺服器正在將結果集傳送到用戶端，將會停止這個動作。 如果用戶端不想使用結果集，則呼叫**issabort:: Abort**之前釋放資料列集將會加速資料列集的版本中，但如果沒有開啟的交易，而且 XACT_ABORT 為 ON，將會回復交易時**Issabort:: Abort**稱為  
  
 之後**issabort:: Abort**傳回 S_OK 時，相關聯**IMultipleResults**介面進入無法使用的狀態並將 db_e_canceled 傳回到所有方法呼叫 (除了所定義的方法**IUnknown**介面) 直到釋放它為止。 如果**IRowset**有取自**IMultipleResults**之前呼叫**中止**、 進入無法使用的狀態，並傳回 DB_E_CANCELED 所有方法呼叫 （除了所定義的方法**IUnknown**介面和**irowset:: Releaserows**) 直到成功呼叫之後釋放它為止**issabort:: Abort**.  
  
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
 發生提供者特定錯誤。詳細資訊，請使用[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)介面。  
  
 E_UNEXPECTED  
 此方法的呼叫是非預期的。 比方說，物件處於廢止狀態因為**issabort:: Abort**已經呼叫過。  
  
 E_OUTOFMEMORY  
 記憶體不足的錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [ISSAbort &#40;OLE DB&#41;](../../database-engine/dev-guide/issabort-ole-db.md)  
  
  