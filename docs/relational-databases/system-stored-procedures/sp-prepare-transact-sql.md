---
title: sp_prepare (Transact SQL) |Microsoft 文件
ms.custom: ''
ms.date: 02/28/2018
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepare
ms.assetid: f328c9eb-8211-4863-bafa-347e1bf7bb3f
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 08e1c0f988d480e7c0c98d0818591734574ece87
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33254362"
---
# <a name="spprepare-transact-sql"></a>sp_prepare (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  準備參數化[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式傳回的陳述式和*處理*執行。 sp_prepare 的叫用方式指定 ID = 11 表格式資料流 (TDS) 封包中的。  
  
 ![文章連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_prepare handle OUTPUT, params, stmt, options  
```  
  
## <a name="arguments"></a>引數  
 *控制代碼*  
 這是 SQL Server 產生*備妥控制代碼*識別項。 *處理*是必要的參數與**int**傳回值。  
  
 *params*  
 識別參數化的陳述式。 *Params*變數的定義會替代陳述式中的參數標記。 *params*是必要的參數呼叫**ntext**， **nchar**，或**nvarchar**輸入值。 如果陳述式未參數化，則輸入 NULL 值。  
  
 *stmt*  
 定義資料指標結果集。 *Stmt*參數是必要而且會呼叫**ntext**， **nchar**，或**nvarchar**輸入值。  
  
 *options*  
 傳回資料指標結果集資料行描述的選擇性參數。 *選項*需要下列 int 輸入的值：  
  
|Value|Description|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
## <a name="examples"></a>範例  
 下列範例會準備及執行簡單陳述式。  
  
```  
Declare @P1 int;  
Exec sp_prepare @P1 output,   
    N'@P1 nvarchar(128), @P2 nvarchar(100)',  
    N'SELECT database_id, name FROM sys.databases WHERE name=@P1 AND state_desc = @P2';  
Exec sp_execute @P1, N'tempdb', N'ONLINE';  
EXEC sp_unprepare @P1;  
```  

  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

