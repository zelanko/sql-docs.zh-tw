---
title: sp_addtabletocontents & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addtabletocontents_TSQL
- sp_addtabletocontents
helpviewer_keywords:
- sp_addtabletocontents
ms.assetid: 2ea27001-74f4-463e-bf1b-b6b5a86b9219
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 991ee7139ae4a323a1d426d1882e4f6b3a4df871
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049718"
---
# <a name="spaddtabletocontents-transact-sql"></a>sp_addtabletocontents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對目前未包括在追蹤資料表內的來源資料表中之任何資料列，將參考插入合併追蹤資料表中。 使用此選項，如果您有大量載入資料所使用的大量**bcp**，不會引發合併追蹤觸發程序。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addtabletocontents [ @table_name = ] 'table_name'  
    [ , [ @owner_name = ] 'owner_name' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @table_name = ] 'table_name'` 為資料表的名稱。 *table_name*已**sysname**，沒有預設值。  
  
`[ @owner_name = ] 'owner_name'` 為資料表的擁有者的名稱。 *owner_name*已**sysname**，預設值是 NULL。  
  
`[ @filter_clause = ] 'filter_clause'` 指定一個篩選子句來控制哪些新載入的資料的資料列應該加入合併追蹤資料表。 *filter_clause*已**nvarchar(4000)** ，預設值是 NULL。 如果*filter_clause*是**null**，所有的大量載入的資料列會加入。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addtabletocontents**只適用於合併式複寫。  
  
 中的資料列*table_name*由參考其**rowguidcol** ，參考會加入合併追蹤資料表。 **sp_addtabletocontents**大量複製資料到利用合併式複寫發行的資料表之後，應該使用。 這個預存程序會起始複製的資料列追蹤，並確定新資料列會併入下一次同步處理中。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addtabletocontents**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
