---
description: sp_dropanonymousagent (Transact-SQL)
title: sp_dropanonymousagent (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropanonymousagent
- sp_dropanonymousagent_TSQL
helpviewer_keywords:
- sp_dropanonymousagent
ms.assetid: 4cb96efa-9358-44a3-a8ee-a7e181bed089
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: d6e687976dab6d526a2413260d2ad2f980001086
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474274"
---
# <a name="sp_dropanonymousagent-transact-sql"></a>sp_dropanonymousagent (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  從發行者卸除在散發者端之複寫監視的匿名代理程式。 這個預存程序執行於任何資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_dropanonymousagent [ @subid= ] sub_id    , [ @type= ] type  
```  
  
## <a name="arguments"></a>引數  
`[ @subid = ] sub_id` 這是匿名訂閱的全域識別碼。 *sub_id* 是 **uniqueidentifier**，沒有預設值。 您可以使用 **sp_helppullsubscription**，在訂閱者端抓取此識別碼。 傳回之結果集的 **subid** 欄位中的值是此全域識別碼。  
  
`[ @type = ] type` 這是訂閱的類型。 *類型* 是 **int**，沒有預設值。 有效的值為 **1** 或 **2**。 如果快照式複寫或使用散發代理程式的異動複寫，請指定 **1**。 如果使用合併代理程式的合併式複寫，請指定 **2**。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_dropanonymousagent** 用於所有類型的複寫中。  
  
 這個預存程序只能用來卸除匿名訂閱代理程式，無法用來卸除已知的訂閱。  
  
## <a name="permissions"></a>權限  
 只有散發資料庫中 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_dropanonymousagent**。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
