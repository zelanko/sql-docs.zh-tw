---
title: sp_repldone (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repldone
- sp_repldone_TSQL
helpviewer_keywords:
- sp_repldone
ms.assetid: 045d3cd1-712b-44b7-a56a-c9438d4077b9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 35cd38269fabba59d257e41141141764b6d4919d
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771108"
---
# <a name="sprepldone-transact-sql"></a>sp_repldone (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  更新用來識別伺服器最後分散式交易的記錄。 這個預存程序執行於發行集資料庫的發行者端。  
  
> [!CAUTION]  
>  如果您手動執行**sp_repldone** , 您可以讓傳遞之交易的順序和一致性失效。 **sp_repldone**只能用於疑難排解複寫支援專業人員所導向的複寫。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_repldone [ @xactid= ] xactid   
        , [ @xact_seqno= ] xact_seqno   
    [ , [ @numtrans= ] numtrans ]   
    [ , [ @time= ] time   
    [ , [ @reset= ] reset ]  
```  
  
## <a name="arguments"></a>引數  
`[ @xactid = ] xactid`這是伺服器上次分散式交易的第一筆記錄的記錄序號 (LSN)。 *xactid*是**binary (10)** , 沒有預設值。  
  
`[ @xact_seqno = ] xact_seqno`這是伺服器最後一次分散式交易的最後一筆記錄的 LSN。 *xact_seqno*是**binary (10)** , 沒有預設值。  
  
`[ @numtrans = ] numtrans`這是散發的交易數。 *numtrans*是**int**, 沒有預設值。  
  
`[ @time = ] time`這是散發最後一批交易所需的毫秒數 (如有提供)。 *time*是**int**, 沒有預設值。  
  
`[ @reset = ] reset`這是重設狀態。 *reset*是**int**, 沒有預設值。 如果是**1**, 記錄中所有複寫的交易都會標示為已散發。 如果是**0**, 交易記錄會重設為第一個複寫的交易, 且不會將任何複寫的交易標示為已散發。 只有當*xactid*和*XACT_SEQNO*都是 Null 時, *reset*才有效。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或**1** (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_repldone**用於異動複寫中。  
  
 記錄讀取器進程會使用**sp_repldone**來追蹤已散發的交易。  
  
 透過**sp_repldone**, 您可以手動指示伺服器已複寫交易 (傳送至「散發者」)。 它也可讓您變更標示成下一項等待複寫的交易。 您可以在複寫交易清單中，向前或向後移動。 (所有小於或等於這項交易的交易都會標示成已散發。)  
  
 您可以使用**sp_repltrans**或**sp_replcmds**來取得必要的參數*xactid*和*xact_seqno* 。  
  
## <a name="permissions"></a>Permissions  
 **系統管理員 (sysadmin** ) 固定伺服器角色或**db_owner**固定資料庫角色的成員, 可以執行**sp_repldone**。  
  
## <a name="examples"></a>範例  
 當*xactid*是 null 時, *xact_seqno*是 null, 而*reset*是**1**, 記錄中所有複寫的交易都會標示為已散發。 當交易記錄中有不再有效的複寫交易，且您要截斷記錄時，這便非常有用，例如：  
  
```  
EXEC sp_repldone @xactid = NULL, @xact_segno = NULL, @numtrans = 0,     @time = 0, @reset = 1  
```  
  
> [!CAUTION]  
>  如果出現緊急狀況，您可以利用這個程序，以便在有交易暫止複寫存在時截斷交易記錄。  
  
## <a name="see-also"></a>另請參閱  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
