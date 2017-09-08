---
title: "KILL QUERY NOTIFICATION SUBSCRIPTION (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- KILL QUERY NOTIFICATION SUBSCRIPTION
- KILL_QUERY_NOTIFICATION_SUBSCRIPTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- KILL QUERY NOTIFICATION SUBSCRIPTION statement
- removing subscriptions
- subscriptions [SQL Server query notifications], stopping
- query notifications [SQL Server], subscriptions
ms.assetid: 8aeadf51-286c-4748-bef2-d25858b250bf
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3c6937424d2cd68095952c3faba2a446488e9122
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="kill-query-notification-subscription-transact-sql"></a>KILL QUERY NOTIFICATION SUBSCRIPTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從執行個體移除查詢通知訂閱。 這個陳述式可以移除特定的訂閱或所有的訂閱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
KILL QUERY NOTIFICATION SUBSCRIPTION   
   { ALL | subscription_id }  
```  
  
## <a name="arguments"></a>引數  
 ALL  
 移除執行個體中所有的訂閱。  
  
 *subscription_id*  
 移除訂用帳戶 id 與訂用帳戶*subscription_id*。  
  
## <a name="remarks"></a>備註  
 KILL QUERY NOTIFICATION SUBSCRIPTION 陳述式會移除查詢通知訂閱，但不產生通知訊息。  
  
 *subscription_id*動態管理檢視中所示，為訂用帳戶 id [sys.dm_qn_subscriptions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/query-notifications-sys-dm-qn-subscriptions.md).  
  
 如果指定的訂閱識別碼不存在，陳述式便會產生錯誤。  
  
## <a name="permissions"></a>Permissions  
 若要執行此陳述式的權限僅限於成員**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
  
### <a name="a-removing-all-query-notification-subscriptions-in-the-instance"></a>A. 移除執行個體中所有的查詢通知訂閱  
 下列範例會移除執行個體中所有的查詢通知訂閱。  
  
```  
KILL QUERY NOTIFICATION SUBSCRIPTION ALL ;  
```  
  
### <a name="b-removing-a-single-query-notification-subscription"></a>B. 移除單一查詢通知訂閱  
 下列範例會移除識別碼為 `73` 的查詢通知訂閱。  
  
```  
KILL QUERY NOTIFICATION SUBSCRIPTION 73 ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_qn_subscriptions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/query-notifications-sys-dm-qn-subscriptions.md)  
  
  

