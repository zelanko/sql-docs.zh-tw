---
title: sp_repldone (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_repldone
- sp_repldone_TSQL
helpviewer_keywords:
- sp_repldone
ms.assetid: 045d3cd1-712b-44b7-a56a-c9438d4077b9
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: afc84474a5aff0fff81efc702239dfa3f0ff85e7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sprepldone-transact-sql"></a>sp_repldone (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新用來識別伺服器最後分散式交易的記錄。 這個預存程序執行於發行集資料庫的發行者端。  
  
> [!CAUTION]  
>  如果您執行**sp_repldone**手動，您可能會讓失效的順序與已傳遞的交易一致性。 **sp_repldone**應該只用於複寫在資深的複寫支援專家的疑難排解。  
  
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
 [  **@xactid=**] *xactid*  
 是伺服器最後分散式交易第一筆記錄序號 (LSN)。 *xactid*是**binary （10)**，沒有預設值。  
  
 [  **@xact_seqno=**] *xact_seqno*  
 是伺服器最後分散式交易的最後一個記錄的 LSN。 *xact_seqno*是**binary （10)**，沒有預設值。  
  
 [  **@numtrans=**] *numtrans*  
 是分散式的交易數目。 *numtrans*是**int**，沒有預設值。  
  
 [  **@time=**]*時間*  
 這是散發最後一批交易所需要的毫秒數 (如果有提供)。 *時間*是**int**，沒有預設值。  
  
 [  **@reset=**]*重設*  
 這是重設狀態。 *重設*是**int**，沒有預設值。 如果**1**、 所有複寫記錄檔中的交易都會標示成已散發。 如果**0**、 交易記錄會重設為第一個複寫的交易，並沒有複寫的交易標示成已散發。 *重設*有效時，才兩者*xactid*和*xact_seqno*都為 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_repldone**用於異動複寫中。  
  
 **sp_repldone**用來追蹤已散發的交易記錄讀取器程序。  
  
 與**sp_repldone**，您可以手動告知伺服器尚未複寫 （傳送到 「 散發者 」） 的交易。 它也可讓您變更標示成下一項等待複寫的交易。 您可以在複寫交易清單中，向前或向後移動。 (所有小於或等於這項交易的交易都會標示成已散發。)  
  
 必要的參數*xactid*和*xact_seqno*可以使用來取得**sp_repltrans**或**sp_replcmds**。  
  
## <a name="permissions"></a>Permissions  
 成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_repldone**。  
  
## <a name="examples"></a>範例  
 當*xactid*是 NULL， *xact_seqno*是 NULL，和*重設*是**1**、 所有複寫記錄檔中的交易都會標示成已散發。 當交易記錄中有不再有效的複寫交易，且您要截斷記錄時，這便非常有用，例如：  
  
```  
EXEC sp_repldone @xactid = NULL, @xact_segno = NULL, @numtrans = 0,     @time = 0, @reset = 1  
```  
  
> [!CAUTION]  
>  如果出現緊急狀況，您可以利用這個程序，以便在有交易暫止複寫存在時截斷交易記錄。  
  
## <a name="see-also"></a>另請參閱  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_replflush &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
