---
title: srv_paramsetoutput (擴充預存程序 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paramsetoutput
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramsetoutput
ms.assetid: f2810e19-e513-458b-8925-5756b6ee1313
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 26dd8add089f27c3ea9db22204548196bc887faf
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53357960"
---
# <a name="srvparamsetoutput-extended-stored-procedure-api"></a>srv_paramsetoutput (擴充預存程序 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 設定傳回參數的值。 這個函式會取代 **srv_paramset** 函式。  
  
## <a name="syntax"></a>語法  
  
```  
  
int srv_paramsetoutput (  
SRV_PROC *  
srvproc  
,  
int  
n  
,  
BYTE *  
pbData  
,  
ULONG   
cbLen  
,  
BOOL  
fNull   
);  
  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 這是用戶端連接的控制代碼。  
  
 *n*  
 這是要設定之參數的序數。 第一個參數是 1。  
  
 *pbData*  
 這是指向要當做程序傳回參數傳回給用戶端之資料值的指標。  
  
 *cbLen*  
 這是要傳回之資料的實際長度。 如果參數的資料類型會指定固定長度的值，而且不允許 null 值 (例如 *srvbit* 或 *srvint1*)，則會忽略 *cbLen*。 如果 *fNull* 為 FALSE，0 的值代表長度為零的資料。  
  
 *fNull*  
 這是一個旗標，可指出傳回參數的值是否為 NULL。 如果此參數應該設定為 NULL，請將此旗標設定為 TRUE。 預設值為 FALSE。 如果 *fNull* 設定為 TRUE，*cbLen* 應該設定為 0，否則此函式將會失敗。  
  
## <a name="returns"></a>傳回值  
 如果成功設定參數資訊，則會傳回 SUCCEED，否則會傳回 FAIL。 在以下情況下會傳回 FAIL  
  
-   此參數不是傳回參數，或是  
  
-   *cbLen* 引數無效。  
  
## <a name="remarks"></a>備註  
 **安全性注意事項**：您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
  
