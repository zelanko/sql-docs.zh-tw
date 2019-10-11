---
title: sp_posttracertoken （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- posttracerttoken
- posttracerttoken_TSQL
- sp_posttracertoken
- sp_posttracertoken_TSQL
helpviewer_keywords:
- sp_posttracertoken
ms.assetid: 24da5cd2-1c45-475e-93db-5bdf660f1c2c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7629c25264f0b45d68e29e947b1d5c40d02707e7
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041179"
---
# <a name="sp_posttracertoken-transact-sql"></a>sp_posttracertoken (Transact-SQL)
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
`[ @publication = ] 'publication'` 是測量延遲的發行集名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @tracer_token_id = ] _tracer_token_id OUTPUT` 是所插入之追蹤 token 的識別碼。 *tracer_token_id*是**int** ，預設值是 Null，它是一個 OUTPUT 參數。 此值可以用來執行[ &#40;sp_helptracertokenhistory transact-sql&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)或[sp_deletetracertokenhistory &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md) ，而不需要先執行[sp_helptracertokens transact-sql &#40;&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md).  
  
`[ @publisher = ] 'publisher'` 指定非 @no__t 1 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *publisher*是**sysname**，預設值是 Null，而且不應該為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者指定。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_posttracertoken**用於異動複寫中。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-posttracertoken-trans_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_posttracertoken**。  
  
## <a name="see-also"></a>另請參閱  
 [針對異動複寫測量延遲及驗證連接](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
