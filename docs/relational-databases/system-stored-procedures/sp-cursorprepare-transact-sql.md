---
title: "sp_cursorprepare (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs: TSQL
helpviewer_keywords: sp_cursor_prepare
ms.assetid: 6207e110-f4bf-4139-b3ec-b799c9cb3ad7
caps.latest.revision: "10"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 87d9a5eb64f10e07549a282dc77dc21d219b6584
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spcursorprepare-transact-sql"></a>sp_cursorprepare (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將資料指標陳述式或批次編譯成一個執行計畫，但是不建立資料指標。 之後 sp_cursorexecute 可以使用編譯過的陳述式。 這個程序與 sp_cursorexecute，結合具有相同的函數 sp_cursoropen，但是會分成兩個階段。 sp_cursorprepare 的叫用方式指定 ID = 3，在表格式資料流 (TDS) 封包中的。  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_cursorprepare prepared_handle OUTPUT, params , stmt , options  
    [ , scrollopt[ , ccopt]]  
```  
  
## <a name="arguments"></a>引數  
 *prepared_handle*  
 SQL Server 產生準備*處理*傳回整數值的識別項。  
  
> [!NOTE]  
>  *prepared_handle*後續會提供給 sp_cursorexecute 程序以便開啟資料指標。 一旦建立控制代碼之後，在您登出或是透過 sp_cursorunprepare 程序明確將它移除之前，它都會存在。  
  
 *params*  
 識別參數化的陳述式。 *Params*變數的定義會替代陳述式中的參數標記。 *params*是必要的參數呼叫**ntext**， **nchar**，或**nvarchar**輸入值。 如果陳述式未參數化，則輸入 NULL 值。  
  
> [!NOTE]  
>  使用**ntext**字串做為輸入值時*stmt*參數化和*scrollopt* PARAMETERIZED_STMT 值為 ON。  
  
 *陳述式*  
 定義資料指標結果集。 *Stmt*參數是必要而且會呼叫**ntext**， **nchar**或**nvarchar**輸入值。  
  
> [!NOTE]  
>  指定的規則*stmt*值會與 sp_cursoropen，發生例外狀況的相同， *stmt*字串資料類型必須是**ntext**。  
  
 *選項*  
 傳回資料指標結果集資料行描述的選擇性參數。 *選項*必須符合下列需求**int**輸入值。  
  
|值|Description|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 捲動選項。 *scrollopt*是需要下列其中一個選擇性參數**int**輸入值。  
  
|值|Description|  
|-----------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
|0x10|FAST_FORWARD|  
|0x1000|PARAMETERIZED_STMT|  
|0x2000|AUTO_FETCH|  
|0x4000|AUTO_CLOSE|  
|0x8000|CHECK_ACCEPTED_TYPES|  
|0x10000|KEYSET_ACCEPTABLE|  
|0x20000|DYNAMIC_ACCEPTABLE|  
|0x40000|FORWARD_ONLY_ACCEPTABLE|  
|0x80000|STATIC_ACCEPTABLE|  
|0x100000|FAST_FORWARD_ACCEPTABLE|  
  
 因為要求的值可能不適合用於所定義的資料指標*stmt*，這個參數會當做輸入和輸出。 在這類情況下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會指派適合的值。  
  
 *ccopt*  
 並行控制選項。 *ccopt*是需要下列其中一個選擇性參數**int**輸入值。  
  
|值|Description|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS (之前稱為 LOCKCC)|  
|0x0004|**開放式**（之前稱為 OPTCC）|  
|0x0008|OPTIMISTIC (之前稱為 OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 如同*scrollpt*，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以指派不同的值要求。  
  
## <a name="remarks"></a>備註  
 RPC 狀態參數是下列其中一項：  
  
|值|描述|  
|-----------|-----------------|  
|0|成功|  
|0x0001|失敗|  
|1FF6|無法傳回中繼資料。<br /><br /> 注意： 這是因為陳述式不會產生結果集;例如，它是 INSERT 或 DDL 陳述式。|  
  
## <a name="examples"></a>範例  
 當*stmt*參數化和*scrollopt* PARAMETERIZED_STMT 值為 ON，字串的格式如下所示：  
  
 { *\<本機變數名稱 >**\<資料型別 >* } [，...*n* ]  
  
## <a name="see-also"></a>請參閱＜  
 [sp_cursorexecute &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [sp_cursoropen &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorunprepare &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursorunprepare-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
