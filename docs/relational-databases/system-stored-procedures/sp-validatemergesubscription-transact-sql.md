---
title: sp_validatemergesubscription (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_validatemergesubscription
- sp_validatemergesubscription_TSQL
helpviewer_keywords:
- sp_validatemergesubscription
ms.assetid: d73ad03c-e5b3-4606-a0ee-7d75e12762a6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3341bf25e43f73143fa1dd0e66add9f4b86c22bb
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155532"
---
# <a name="sp_validatemergesubscription-transact-sql"></a>sp_validatemergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  執行指定訂閱的驗證。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_validatemergesubscription [@publication=] 'publication'  
        , [ @subscriber = ] 'subscriber'  
        , [ @subscriber_db = ] 'subscriber_db'  
        , [ @level = ] level  
```  
  
## <a name="arguments"></a>引數  
 **[\@發行集 =** ] **'***發行***'**  
 這是發行集的名稱。 *發行*集是**sysname**, 沒有預設值。  
  
`[ @subscriber = ] 'subscriber'`這是訂閱者的名稱。 *訂閱者*是**sysname**, 沒有預設值。  
  
`[ @subscriber_db = ] 'subscriber_db'`這是訂閱資料庫的名稱。 *subscriber_db*是**sysname**, 沒有預設值。  
  
`[ @level = ] level`這是要執行的驗證類型。 *層級*是**Tinyint**, 沒有預設值。 層級可以是下列值之一。  
  
|層級值|描述|  
|-----------------|-----------------|  
|**1**|僅驗證資料列計數。|  
|**2**|資料列計數及總和檢查碼驗證。|  
|**3**|資料列計數及二進位總和檢查碼驗證。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或**1** (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_validatemergesubscription**用於合併式複寫中。  
  
## <a name="permissions"></a>Permissions  
 只有**系統管理員 (sysadmin** ) 固定伺服器角色或**db_owner**固定資料庫角色的成員, 才能夠執行**sp_validatemergesubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [驗證複寫的資料](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_validatemergepublication &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-validatemergepublication-transact-sql.md)  
  
  
