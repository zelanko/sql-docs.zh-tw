---
title: sp_posttracertoken (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedur+I741es
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- posttracerttoken
- posttracerttoken_TSQL
- sp_posttracertoken
- sp_posttracertoken_TSQL
helpviewer_keywords:
- sp_posttracertoken
ms.assetid: 24da5cd2-1c45-475e-93db-5bdf660f1c2c
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b020aa95aa4f07732843cf360048e63f1d99f7cf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="spposttracertoken-transact-sql"></a>sp_posttracertoken (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  這個程序會在發行者端的交易記錄中公佈一個追蹤 Token，且會起始追蹤延遲統計資料的處理程序。 當追蹤 Token 寫入交易記錄時、當記錄讀取器代理程式收取它時，以及當散發代理程式套用它時，會將資訊記錄下來。 這個預存程序執行於發行集資料庫的發行者端。 如需相關資訊，請參閱 [針對異動複寫測量延遲及驗證連接](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_posttracertoken [ @publication = ] 'publication'   
    [ , [ @tracer_token_id = ] tracer_token_id OUTPUT  
    [ , [ @publisher = ] 'publisher'   
```  
  
## <a name="arguments"></a>引數  
 [ **@publication**=] **'***發行集***'**  
 這是在測量延遲的發行集名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@tracer_token_id=** ] *tracer_token_id * * * 輸出**  
 這是插入之追蹤 Token 的識別碼。 *tracer_token_id*是**int**預設值是 NULL，它是一個 OUTPUT 參數。 這個值可以用來執行[sp_helptracertokenhistory &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)或[sp_deletetracertokenhistory &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)不需事先執行[sp_helptracertokens &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md)。  
  
 [  **@publisher=** ] **'***發行者***'**  
 指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *發行者*是**sysname**，預設值是 NULL，而且不應該為指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_posttracertoken**用於異動複寫中。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-posttracertoken-trans_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_posttracertoken**。  
  
## <a name="see-also"></a>另請參閱  
 [針對異動複寫測量延遲及驗證連接](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
