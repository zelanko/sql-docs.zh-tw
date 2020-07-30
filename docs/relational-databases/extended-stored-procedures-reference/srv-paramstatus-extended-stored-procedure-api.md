---
title: srv_paramstatus (擴充預存程序 API) | Microsoft Docs
description: 瞭解 srv_paramstatus 如何傳回特定遠端預存程序呼叫參數的狀態。
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_paramstatus
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paramstatus
ms.assetid: 86cecd45-0b09-42e9-8152-32a12a1c2b7a
author: rothja
ms.author: jroth
ms.openlocfilehash: e55986b0d781b311b050eb5695ca350f7331e25c
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248327"
---
# <a name="srv_paramstatus-extended-stored-procedure-api"></a>srv_paramstatus (擴充預存程序 API)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 傳回特定遠端預存程序呼叫參數的狀態。  
  
## <a name="syntax"></a>語法  
  
```  
  
int srv_paramstatus (  
SRV_PROC *  
srvproc  
,  
int  
n   
);  
```  
  
## <a name="arguments"></a>引數  
 *srvproc*  
 這是 SRV_PROC 結構的指標，也是特定用戶端連接的控制代碼 (在這個狀況之下，該控制代碼會收到遠端預存程序呼叫)。 擴充預存程序 API 程式庫會使用該結構所包含的資訊來管理應用程式與用戶端之間的通訊和資料。  
  
 *n*  
 這指出參數的數目。 第一個參數是數字 1。  
  
## <a name="returns"></a>傳回  
 包含參數之狀態旗標的 **int**。 目前只有一個旗標：如果位元 0 設定為 1，參數為傳回參數。 如果沒有第 *n* 個參數或是沒有任何遠端預存程序，其會傳回 -1。  
  
## <a name="remarks"></a>備註  
 此常式會傳回遠端預存程序呼叫參數的狀態旗標。  
  
 參數包含了在用戶端和應用程式之間傳遞的資料，其中包含遠端預存程序。 用戶端可以將某些參數指定為傳回參數。 這些傳回參數可包含應用程式傳回給用戶端的值。  
  
 目前唯一的狀態旗標為指出參數是否為傳回參數的旗標。  
  
 當遠端預存程序呼叫是用參數產生時，該參數可以依名稱或位置 (未命名) 傳遞。 如果遠端預存程序呼叫是藉由一些依名稱傳遞的參數和一些依位置傳遞的參數來進行時，就會發生錯誤。 如果發生錯誤，仍然會呼叫 SRV_RPC 處理常式，但看起來就好像沒有任何參數， **srv_rpcparams**會傳回0。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
## <a name="see-also"></a>另請參閱  
 [srv_rpcparams &#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-rpcparams-extended-stored-procedure-api.md)  
  
  
