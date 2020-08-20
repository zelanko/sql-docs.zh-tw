---
description: sp_prepexec (Transact-SQL)
title: sp_prepexec (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: b8d6d652c6324344af24b9efbb5b74e3accf203e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473900"
---
# <a name="sp_prepexec-transact-sql"></a>sp_prepexec (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  準備和執行參數化 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語句。 sp_prepexec 結合 sp_prepare 和 sp_execute 的功能。 這項動作是以表格式資料流程中的識別碼 = 13 為 (，TDS) 封包。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_prepexec handle OUTPUT, params , stmt  
    [ , bound param ] [ ,...n]]  
```  
  
## <a name="arguments"></a>引數  
 *處理*  
 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生的 *控制碼* 識別碼。 *控制碼* 是具有 **int** 傳回值的必要參數。  
  
 *params*  
 識別參數化的陳述式。 變數的 *params* 定義會取代為語句中的參數標記。 *params* 是呼叫 **Ntext**、 **Nchar**或 **Nvarchar** 輸入值的必要參數。 如果陳述式未參數化，則輸入 NULL 值。  
  
 *stmt*  
 定義資料指標結果集。 需要 *stmt* 參數，並呼叫 **Ntext**、 **Nchar**或 **Nvarchar** 輸入值。  
  
 *bound_param*  
 指定選擇性使用其他參數。 *bound_param* 會呼叫任何資料類型的輸入值，以指定使用中的其他參數。  
  
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
  
