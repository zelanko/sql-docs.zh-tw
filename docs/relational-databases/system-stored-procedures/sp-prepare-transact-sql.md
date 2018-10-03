---
title: sp_prepare (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 02/28/2018
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepare
ms.assetid: f328c9eb-8211-4863-bafa-347e1bf7bb3f
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 42d5912b67a4039ccd16421413a20763aa8015c5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47644218"
---
# <a name="spprepare-transact-sql"></a>sp_prepare (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  準備參數化[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式，並傳回陳述式*處理*執行。 sp_prepare 的叫用方式指定 ID = 11 中的表格式資料流 (TDS) 封包。  
  
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
 定義資料指標結果集。 *Stmt*為必要參數，呼叫**ntext**， **nchar**，或**nvarchar**輸入值。  
  
 *options*  
 傳回資料指標結果集資料行描述的選擇性參數。 *選項*需要下列的整數輸入的值：  
  
|值|描述|  
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
  
  

