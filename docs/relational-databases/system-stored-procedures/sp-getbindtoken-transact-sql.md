---
title: sp_getbindtoken (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_getbindtoken
- sp_getbindtoken_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_getbindtoken
ms.assetid: 5db87d77-85fa-45a3-a23a-3ea500f9a5ac
caps.latest.revision: 47
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ecf272b61591124b6e7ce920ecf1c8b481a6ac5e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="spgetbindtoken-transact-sql"></a>sp_getbindtoken (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回交易的唯一識別碼。 這個唯一識別碼是利用 sp_bindsession 來繫結工作階段時所用的字串。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用 Multiple Active Result Set (MARS) 或分散式交易。 如需詳細資訊，請參閱[使用 Multiple Active Result Set & #40;MARS & #41;](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md).  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_getbindtoken [@out_token =] 'return_value' OUTPUT   
```  
  
## <a name="arguments"></a>引數  
 [@out_token=]'*return_value*'  
 這是用來繫結工作階段的 Token。 *return_value*是**varchar （255)** 沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 無  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 只有在使用中交易內執行預存程序時，sp_getbindtoken 會傳回有效的語彙基元。 否則，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會傳回錯誤訊息。 例如：  
  
```  
-- Declare a variable to hold the bind token.  
-- No active transaction.  
DECLARE @bind_token varchar(255);  
-- Trying to get the bind token returns an error 3921.  
EXECUTE sp_getbindtoken @bind_token OUTPUT;  
Server: Msg 3921, Level 16, State 1, Procedure sp_getbindtoken, Line 4  
Cannot get a transaction token if there is no transaction active.  
Reissue the statement after a transaction has been started.  
```  
  
 當 sp_getbindtoken 來編列分散式的交易連接開啟的交易，內部[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回相同的 token。 例如：  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @bind_token varchar(255);  
  
BEGIN TRAN;  
  
EXECUTE sp_getbindtoken @bind_token OUTPUT;  
SELECT @bind_token AS Token;  
  
BEGIN DISTRIBUTED TRAN;  
  
EXECUTE sp_getbindtoken @bind_token OUTPUT;  
SELECT @bind_token AS Token;  
```  
  
 兩個 `SELECT` 陳述式都會傳回相同的 Token：  
  
```  
Token  
-----  
PKb'gN5<9aGEedk_16>8U=5---/5G=--  
(1 row(s_) affected)  
  
Token  
-----  
PKb'gN5<9aGEedk_16>8U=5---/5G=--  
(1 row(s_) affected)  
```  
  
 繫結 Token 可以搭配 sp_bindsession 來使用，將新工作階段繫結到相同的交易。 繫結 Token 只在每個 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的本機環境內有效，不同的執行個體並不能共用它。  
  
 若要取得並傳遞繫結 Token，您必須先執行 sp_getbindtoken，再執行 sp_bindsession，才能共用相同的鎖定空間。 如果您取得繫結 Token，就能夠正確執行 sp_bindsession。  
  
> [!NOTE]  
>  我們建議您利用 srv_getbindtoken 開放式資料服務 (Open Data Services) 應用程式開發介面 (API)，從擴充預存程序中取得要使用的繫結 Token。  
  
## <a name="permissions"></a>Permissions  
 需要 public 角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會取得繫結 Token，且會顯示繫結 Token 名稱。  
  
```  
DECLARE @bind_token varchar(255);  
BEGIN TRAN;  
EXECUTE sp_getbindtoken @bind_token OUTPUT;  
SELECT @bind_token AS Token;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Token`  
  
 `----------------------------------------------------------`  
  
 `\0]---5^PJK51bP<1F<-7U-]ANZ`  
  
## <a name="see-also"></a>另請參閱  
 [sp_bindsession & #40;TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-bindsession-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [srv_getbindtoken&#40;擴充預存程序 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-getbindtoken-extended-stored-procedure-api.md)  
  
  
