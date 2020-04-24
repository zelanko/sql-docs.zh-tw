---
title: KILL QUERY NOTIFICATION SUBSCRIPTION
description: 從執行個體移除查詢通知訂閱。 這個陳述式可以移除特定的訂閱或所有的訂閱。
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a4f31f58cdac2032338c2a4a1b6096f1c82070b0
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81636023"
---
# <a name="kill-query-notification-subscription-transact-sql"></a>KILL QUERY NOTIFICATION SUBSCRIPTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從執行個體移除查詢通知訂閱。 這個陳述式可以移除特定的訂閱或所有的訂閱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
  
KILL QUERY NOTIFICATION SUBSCRIPTION   
   { ALL | subscription_id }  
```  
  
## <a name="arguments"></a>引數  
 ALL  
 移除執行個體中所有的訂閱。  
  
 *subscription_id*  
 移除訂閱識別碼為 *subscription_id* 的訂閱。  
  
## <a name="remarks"></a>備註  
 KILL QUERY NOTIFICATION SUBSCRIPTION 陳述式會移除查詢通知訂閱，但不產生通知訊息。  
  
 *subscription_id* 是如動態管理檢視 [sys.dm_qn_subscriptions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/query-notifications-sys-dm-qn-subscriptions.md) 中所顯示的訂閱識別碼。  
  
 如果指定的訂閱識別碼不存在，陳述式便會產生錯誤。  
  
## <a name="permissions"></a>權限  
 只有 **sysadmin** 固定伺服器角色的成員，才有執行這個陳述式的權限。  
  
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
 [sys.dm_qn_subscriptions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/query-notifications-sys-dm-qn-subscriptions.md)  
  
  
