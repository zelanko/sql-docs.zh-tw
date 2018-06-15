---
title: sp_addtabletocontents (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_addtabletocontents_TSQL
- sp_addtabletocontents
helpviewer_keywords:
- sp_addtabletocontents
ms.assetid: 2ea27001-74f4-463e-bf1b-b6b5a86b9219
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 47400ed08fed28f8b2c6a83189cd640b9c727f9a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32988903"
---
# <a name="spaddtabletocontents-transact-sql"></a>sp_addtabletocontents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對目前未包括在追蹤資料表內的來源資料表中之任何資料列，將參考插入合併追蹤資料表中。 使用此選項，如果您有大量載入大量的資料使用**bcp**，不會引發合併追蹤觸發程序。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addtabletocontents [ @table_name = ] 'table_name'  
    [ , [ @owner_name = ] 'owner_name' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@table_name=**] **'***table_name***'**  
 這是資料表的名稱。 *table_name*是**sysname**，沒有預設值。  
  
 [  **@owner_name=**] **'***owner_name***'**  
 這是資料表擁有者的名稱。 *owner_name*是**sysname**，預設值是 NULL。  
  
 [  **@filter_clause=** ] **'***filter_clause***'**  
 指定一個篩選子句來控制哪些新載入的資料列應該加入合併追蹤資料表中。 *filter_clause*是**nvarchar （4000)**，預設值是 NULL。 如果*filter_clause*是**null**，所有的大量載入的資料列會加入。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addtabletocontents**只適用於合併式複寫。  
  
 中的資料列*table_name*由參考其**rowguidcol** ，參考會加入合併追蹤資料表。 **sp_addtabletocontents**大量複製資料到利用合併式複寫發行的資料表之後，應該使用。 這個預存程序會起始複製的資料列追蹤，並確定新資料列會併入下一次同步處理中。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addtabletocontents**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
