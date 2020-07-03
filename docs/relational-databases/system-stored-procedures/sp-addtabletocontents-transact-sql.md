---
title: sp_addtabletocontents （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 928d601fe544432b669b84b8d8a819405bcfbc7e
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85876038"
---
# <a name="sp_addtabletocontents-transact-sql"></a>sp_addtabletocontents (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  針對目前未包括在追蹤資料表內的來源資料表中之任何資料列，將參考插入合併追蹤資料表中。 如果您已使用**bcp**大量載入大量資料，而不會引發合併追蹤觸發程式，請使用此選項。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addtabletocontents [ @table_name = ] 'table_name'  
    [ , [ @owner_name = ] 'owner_name' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @table_name = ] 'table_name'`這是資料表的名稱。 *table_name*是**sysname**，沒有預設值。  
  
`[ @owner_name = ] 'owner_name'`這是資料表擁有者的名稱。 *owner_name*是**sysname**，預設值是 Null。  
  
`[ @filter_clause = ] 'filter_clause'`指定篩選子句，以控制要將新載入的資料列加入合併追蹤資料表中。 *filter_clause*是**Nvarchar （4000）**，預設值是 Null。 如果*filter_clause*為**null**，則會加入所有大量載入的資料列。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addtabletocontents**僅用於合併式複寫中。  
  
 *Table_name*中的資料列是由其**rowguidcol**所參考，而參考則會加入合併追蹤資料表中。 將資料大量複製到使用合併式複寫所發行的資料表之後，應該使用**sp_addtabletocontents** 。 這個預存程序會起始複製的資料列追蹤，並確定新資料列會併入下一次同步處理中。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_addtabletocontents**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
