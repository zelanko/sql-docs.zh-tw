---
title: sp_scriptdynamicupdproc (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_scriptdynamicupdproc_TSQL
- sp_scriptdynamicupdproc
helpviewer_keywords:
- sp_scriptdynamicupdproc
ms.assetid: b4c18863-ed92-4aa2-a04f-7ed832fc9e07
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b548223d520696f7c7a2b48f4010247666d41597
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="spscriptdynamicupdproc-transact-sql"></a>sp_scriptdynamicupdproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  產生建立動態更新預存程序的 CREATE PROCEDURE 陳述式。 自訂預存程序內的 UPDATE 陳述式是根據指示要變更的資料行之 MCALL 語法來動態建置的。 如果訂閱資料表的索引數目在成長，且所變更的資料行數目不多，請使用這個預存程序。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_scriptdynamicupdproc [ @artid =] artid  
```  
  
## <a name="arguments"></a>引數  
 [  **@artid=**] *artid*  
 這是發行項識別碼。 *artid*是**int**，沒有預設值。  
  
## <a name="result-sets"></a>結果集  
 傳回的結果集包含單一**nvarchar （4000)**資料行。 這個結果集形成用來建立自訂預存程序的完整 CREATE PROCEDURE 陳述式。  
  
## <a name="remarks"></a>備註  
 **sp_scriptdynamicupdproc**用於異動複寫中。 預設 MCALL 指令碼邏輯包括 UPDATE 陳述式內的所有資料行，且利用點陣圖來判斷已變更的資料行。 如果資料行並未變更，資料行會重設為其本身，這通常不會有問題。 如果資料行已建立索引，就會進行額外的處理。 動態方法只包括已變更的資料行，這會提供最佳的 UPDATE 字串。 不過，當建立動態 UPDATE 陳述式時，會在執行階段進行額外的處理。 我們建議您測試動態和靜態方法，然後再選擇最佳方案。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_scriptdynamicupdproc**。  
  
## <a name="examples"></a>範例  
 這個範例會建立一個發行項 (與*artid*設**1**) 上**作者**資料表中**pubs**資料庫，並指定更新陳述式是執行的自訂程序：  
  
```  
'MCALL sp_mupd_authors'  
```  
  
 產生在訂閱者端的散發代理程式將藉由執行在發行者端的下列預存程序，來執行的自訂預存程序：  
  
```  
EXEC sp_scriptdynamicupdproc @artid = '1'  
  
The statement returns:  
  
CREATE PROCEDURE [sp_mupd_authors]   
  @c1 varchar(11),@c2 varchar(40),@c3 varchar(20),@c4 char(12),@c5 varchar(40),@c6 varchar(20),  
  @c7 char(2),@c8 char(5),@c9 bit,@pkc1 varchar(11),@bitmap binary(2)  
as  
  
declare @stmt nvarchar(4000), @spacer nvarchar(1)  
SELECT @spacer =N''  
SELECT @stmt = N'UPDATE [authors] SET '  
  
if substring(@bitmap,1,1) & 2 = 2  
begin  
  select @stmt = @stmt + @spacer + N'[au_lname]' + N'=@2'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 4 = 4  
begin  
  select @stmt = @stmt + @spacer + N'[au_fname]' + N'=@3'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 8 = 8  
begin  
  select @stmt = @stmt + @spacer + N'[phone]' + N'=@4'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 16 = 16  
begin  
  select @stmt = @stmt + @spacer + N'[address]' + N'=@5'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 32 = 32  
begin  
  select @stmt = @stmt + @spacer + N'[city]' + N'=@6'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 64 = 64  
begin  
  select @stmt = @stmt + @spacer + N'[state]' + N'=@7'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 128 = 128  
begin  
  select @stmt = @stmt + @spacer + N'[zip]' + N'=@8'  
  select @spacer = N','  
end  
if substring(@bitmap,2,1) & 1 = 1  
begin  
  select @stmt = @stmt + @spacer + N'[contract]' + N'=@9'  
  select @spacer = N','  
end  
select @stmt = @stmt + N' where [au_id] = @1'  
exec sp_executesql @stmt, N' @1 varchar(11),@2 varchar(40),@3 varchar(20),@4 char(12),@5 varchar(40),  
                             @6 varchar(20),@7 char(2),@8 char(5),@9 bit',@pkc1,@c2,@c3,@c4,@c5,@c6,@c7,@c8,@c9  
  
if @@rowcount = 0  
   if @@microsoftversion>0x07320000  
      exec sp_MSreplraiserror 20598  
```  
  
 在執行這個預存程序之後，您可以利用產生的指令碼來手動建立在訂閱者端的預存程序。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
