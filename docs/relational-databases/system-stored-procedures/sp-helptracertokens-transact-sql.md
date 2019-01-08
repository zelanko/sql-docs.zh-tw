---
title: sp_helptracertokens & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helptracertokens
- sp_helptracertokens_TSQL
helpviewer_keywords:
- sp_helptracertokens
ms.assetid: 61f27234-531d-4b37-8fa3-fe4c32e6f521
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f521f416c7415d2a27554e7f3d91f5df89023798
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210407"
---
# <a name="sphelptracertokens-transact-sql"></a>sp_helptracertokens (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對插入發行集以判斷延遲的每個追蹤 Token，各傳回一個資料列。 這個預存程序是在發行集資料庫的發行者端，或散發資料庫的散發者端執行。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helptracertokens [ @publication = ] 'publication'   
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@publication=** ] **'***發行集***'**  
 這是插入追蹤 Token 的發行集名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [  **@publisher=** ] **'***發行者***'**  
 發行者的名稱。 *發行者*已**sysname**，預設值是 NULL。  
  
> [!NOTE]
>  這個參數應該只能指定為非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 發行集資料庫的名稱。 *publisher_db*已**sysname**，預設值是 NULL。 如果預存程序執行於發行者端，則會忽略這個參數。  
  
## <a name="result-set"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**tracer_id**|**int**|識別追蹤 Token 記錄。|  
|**publisher_commit**|**datetime**|在發行集資料庫的發行者端認可 Token 記錄的日期和時間。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helptracertokens**用於異動複寫中。  
  
 **sp_helptracertokens**用來執行時取得追蹤 token 識別碼[sp_helptracertokenhistory &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_tracertokens](../../relational-databases/replication/codesnippet/tsql/sp-helptracertokens-tran_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定伺服器角色**db_owner**固定資料庫角色，在發行集資料庫中，或**db_owner**固定的資料庫或**replmonitor**散發資料庫中的角色可以執行**sp_helptracertokenhistory**。  
  
## <a name="see-also"></a>另請參閱  
 [針對異動複寫測量延遲及驗證連線](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [sp_deletetracertokenhistory &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md)  
  
  
