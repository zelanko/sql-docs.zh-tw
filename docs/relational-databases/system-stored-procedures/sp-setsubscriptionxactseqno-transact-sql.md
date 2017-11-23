---
title: "sp_setsubscriptionxactseqno (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_setsubscriptionxactseqno
- sp_setsubscriptionxactseqno_TSQL
helpviewer_keywords: sp_setsubscriptionxactseqno
ms.assetid: cdb4e0ba-5370-4905-b03f-0b0c6f080ca6
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aab7bf1c5fb7653f4b61af1912af7de3454bf776
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spsetsubscriptionxactseqno-transact-sql"></a>sp_setsubscriptionxactseqno (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在疑難排解期間，用來指定在訂閱者端的散發代理程式將套用之下一項交易的記錄序號 (LSN)，使代理程式略過失敗的交易。 這個預存程序執行於訂閱資料庫的訂閱者端。 不支援非 SQL Server 訂閱者使用這個項目。  
  
> [!CAUTION]  
>  不正確使用這個預存程序或指定了不正確的 LSN 值，散發代理程式可能會還原訂閱者端先前所套用的變更，也可能會略過所有其餘變更。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_setsubscriptionxactseqno [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @xact_seqno = ] xact_seqno   
```  
  
## <a name="arguments"></a>引數  
 [  **@publisher=** ] **'***發行者***'**  
 這是發行者的名稱。 *發行者*是**sysname**，沒有預設值。  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 這是發行集資料庫的名稱。 *publisher_db*是**sysname**，沒有預設值。 針對非 SQL Server 發行者， *publisher_db*是散發資料庫的名稱。  
  
 [  **@publication=** ] **'***發行集***'**  
 這是發行集的名稱。 *發行集*是**sysname**，沒有預設值。 當一個以上的發行集所共用散發代理程式時，您必須指定 ALL 值*發行集*。  
  
 [  **@xact_seqno=** ] *xact_seqno*  
 這是訂閱者端所要套用的散發者端之下一項交易的 LSN。 *xact_seqno*是**varbinary （16)**，沒有預設值。  
  
## <a name="result-set"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**原始 XACT_SEQNO**|**varbinary （16)**|訂閱者端所要套用之下一項交易的原始 LSN。|  
|**更新的 XACT_SEQNO**|**varbinary （16)**|訂閱者端所要套用之下一項交易的更新 LSN。|  
|**訂用帳戶資料流計數**|**int**|在上一次同步處理期間所用的訂閱資料流數目。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_setsubscriptionxactseqno**用於異動複寫中。  
  
 **sp_setsubscriptionxactseqno**不能在對等的異動複寫拓撲。  
  
 **sp_setsubscriptionxactseqno**可用來略過導致錯誤的特定交易時在訂閱者端套用。 失敗時之後停止散發代理程式,，請連絡[sp_helpsubscriptionerrors &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriptionerrors-transact-sql.md)在散發者上，擷取失敗的交易的 xact_seqno 值，然後再呼叫**sp_setsubscriptionxactseqno**，傳遞此值，以進行*xact_seqno*。 這可以確保只會處理在這個 LSN 之後的命令。  
  
 指定的值為**0**如*xact_seqno*散發資料庫中的所有暫止命令傳遞給訂閱者。  
  
 **sp_setsubscriptionxactseqno**如果散發代理程式會使用多個訂閱資料流可能會失敗。  
  
 當發生這個錯誤時，您必須利用單一訂閱資料流來執行散發代理程式。 如需詳細資訊，請參閱 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_setsubscriptionxactseqno**。  
  
  
