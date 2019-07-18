---
title: srv_paraminfo (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paraminfo
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paraminfo
ms.assetid: ee2afd4e-0d91-462b-9403-98d481546330
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f3c89eb2e6f810902e28e01c7e5ffbcdcc0375c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127180"
---
# <a name="srvparaminfo-extended-stored-procedure-api"></a>srv_paraminfo (擴充預存程序 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 傳回有關參數的資訊。 這個函式會取代以下函式：[srv_paramtype](srv-paramtype-extended-stored-procedure-api.md)、[srv_paramlen](srv-paramlen-extended-stored-procedure-api.md)、[srv_parammaxlen](srv-parammaxlen-extended-stored-procedure-api.md) 和 [srv_paramdata](srv-paramdata-extended-stored-procedure-api.md)。 **srv_paraminfo** 支援[資料類型](data-types-extended-stored-procedure-api.md)中的資料類型和零長度的資料。  
  
## <a name="syntax"></a>語法  
  
```  
  
int srv_paraminfo (  
SRV_PROC *  
srvproc  
,  
int  
n  
,  
BYTE *  
pbType  
,  
ULONG *  
pcbMaxLen  
,  
ULONG *  
pcbActualLen  
,  
BYTE *  
pbData  
,  
BOOL *  
pfNull  
);  
  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 用戶端連接的控制代碼。  
  
 *n*  
 要設定之參數的序數。 第一個參數是 1。  
  
 *pbType*  
 參數的資料類型。  
  
 *pcbMaxLen*  
 參數之最大長度的指標。  
  
 *pcbActualLen*  
 參數之實際長度的指標。 0 (\**pcbActualLen* == 0) 的值表示長度為零的資料 (如果 **pfNull* 設定為 FALSE)。  
  
 *pbData*  
 參數資料之緩衝區的指標。 如果 *pbData* 不是 NULL，擴充預存程序 API 會將 \**pcbActualLen* 位元組的資料寫入 \**pbData*。 如果 *pbData* 為 NULL，則不會將任何資料寫入 \**pbData*，但此函式會傳回 \**pbType*、\**pcbMaxLen*、\**pcbActualLen* 和 **pfNull*。 此緩衝區的記憶體必須由應用程式管理。  
  
 *pfNull*  
 null 旗標的指標。如果參數值為 NULL， **pfNull* 會設定為 TRUE。  
  
## <a name="returns"></a>傳回值  
 如果成功取得參數資訊，則會傳回 SUCCEED，否則會傳回 FAIL。 目前沒有任何遠端預存程序，且沒有第 *n* 個遠端預存程序參數時，會傳回 FAIL。  
  
## <a name="remarks"></a>備註  
 **安全性注意事項**：您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另請參閱  
 [擴充預存程序程式設計人員參考](database-engine-extended-stored-procedures-reference.md)  
  
  
