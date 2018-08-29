---
title: sp_cursorprepare (TRANSACT-SQL) |Microsoft Docs
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
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_prepare
ms.assetid: 6207e110-f4bf-4139-b3ec-b799c9cb3ad7
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 32e045fe8cc12a8419e94759176e2871db2d2422
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43036524"
---
# <a name="spcursorprepare-transact-sql"></a>sp_cursorprepare (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將資料指標陳述式或批次編譯成一個執行計畫，但是不建立資料指標。 之後 sp_cursorexecute 可以使用編譯過的陳述式。 這個程序與 sp_cursorexecute，結合具有相同的函數 sp_cursoropen，但是會分成兩個階段。 sp_cursorprepare 的叫用方式指定 ID = 3，在表格式資料流 (TDS) 封包中的。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_cursorprepare prepared_handle OUTPUT, params , stmt , options  
    [ , scrollopt[ , ccopt]]  
```  
  
## <a name="arguments"></a>引數  
 *prepared_handle*  
 SQL Server 產生備妥*處理*傳回整數值的識別碼。  
  
> [!NOTE]  
>  *prepared_handle*後續會提供給 sp_cursorexecute 程序以便開啟資料指標。 一旦建立控制代碼之後，在您登出或是透過 sp_cursorunprepare 程序明確將它移除之前，它都會存在。  
  
 *params*  
 識別參數化的陳述式。 *Params*變數的定義會替代陳述式中的參數標記。 *params*是必要的參數呼叫**ntext**， **nchar**，或**nvarchar**輸入值。 如果陳述式未參數化，則輸入 NULL 值。  
  
> [!NOTE]  
>  使用**ntext**字串做為輸入值時*stmt*已參數化而*scrollopt* PARAMETERIZED_STMT 值為 ON。  
  
 *stmt*  
 定義資料指標結果集。 *Stmt*為必要參數，呼叫**ntext**， **nchar**或是**nvarchar**輸入值。  
  
> [!NOTE]  
>  指定的規則*stmt*都與 sp_cursoropen，發生例外狀況的相同的值， *stmt*字串資料類型必須是**ntext**。  
  
 *options*  
 傳回資料指標結果集資料行描述的選擇性參數。 *選項*需要下列**int**輸入值。  
  
|值|描述|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 捲動選項。 *scrollopt*是選擇性參數，它需要下列其中一項**int**輸入值。  
  
|值|描述|  
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
  
 因為要求的值可能不適合所定義的資料指標*stmt*，此參數會當做輸入和輸出。 在這類情況下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會指派適合的值。  
  
 *ccopt*  
 並行控制選項。 *ccopt*是選擇性參數，它需要下列其中一項**int**輸入值。  
  
|值|描述|  
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
|1FF6|無法傳回中繼資料。<br /><br /> 注意： 這是因為該陳述式不會產生結果集;比方說，它是在 INSERT 或 DDL 陳述式。|  
  
## <a name="examples"></a>範例  
 當*stmt*已參數化而*scrollopt* PARAMETERIZED_STMT 值是 ON，字串的格式如下所示：  
  
 { *\<本機變數名稱 > * *\<資料類型 >* } [，...*n* ]  
  
## <a name="see-also"></a>另請參閱  
 [sp_cursorexecute &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [sp_cursoropen &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorunprepare &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-cursorunprepare-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
