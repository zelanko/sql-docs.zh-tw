---
title: sp_prepexec （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepexec
- sp_cursor_prepexec_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepexec
ms.assetid: f9141850-a62b-43bf-8e46-b2f92b75ca56
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ab7c13befad3c1780e067639838efa7434c57f53
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85645894"
---
# <a name="sp_prepexec-transact-sql"></a>sp_prepexec (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  準備和執行參數化 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語句。 sp_prepexec 結合 sp_prepare 和 sp_execute 的功能。 此動作是由表格式資料流程（TDS）封包中的 ID = 13 所叫用。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_prepexec handle OUTPUT, params , stmt  
    [ , bound param ] [ ,...n]]  
```  
  
## <a name="arguments"></a>引數  
 *圖*  
 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生的*控制碼*識別碼。 *handle*是具有**int**傳回值的必要參數。  
  
 *params*  
 識別參數化的陳述式。 變數的*params*定義會取代語句中的參數標記。 *params*是針對**Ntext**、 **Nchar**或**Nvarchar**輸入值呼叫的必要參數。 如果陳述式未參數化，則輸入 NULL 值。  
  
 *把*  
 定義資料指標結果集。 *Stmt*參數是必要的，而且會呼叫**Ntext**、 **Nchar**或**Nvarchar**輸入值。  
  
 *bound_param*  
 指定選擇性使用其他參數。 *bound_param*會呼叫任何資料類型的輸入值，以指定使用中的其他參數。  
  
## <a name="examples"></a>範例  
 下列範例會準備並執行簡單的語句：  
  
```  
Declare @Out int;  
EXEC sp_prepexec @Out output,   
    N'@P1 nvarchar(128), @P2 nvarchar(100)',  
    N'SELECT database_id, name  
      FROM sys.databases  
      WHERE name=@P1 AND state_desc = @P2',   
          @P1 = 'tempdb', @P2 = 'ONLINE';   
EXEC sp_unprepare @Out;  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_prepare &#40;交易 SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_execute &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-execute-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
