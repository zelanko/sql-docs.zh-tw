---
title: sp_cursorprepare （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_prepare
ms.assetid: 6207e110-f4bf-4139-b3ec-b799c9cb3ad7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 641086797c9d6b8ddf6a86a83de1b5d7b69dcb39
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831708"
---
# <a name="sp_cursorprepare-transact-sql"></a>sp_cursorprepare (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將資料指標陳述式或批次編譯成一個執行計畫，但是不建立資料指標。 之後 sp_cursorexecute 可以使用編譯過的陳述式。 此程式與 sp_cursorexecute 結合，具有與 sp_cursoropen 相同的功能，但會分割成兩個階段。 sp_cursorprepare 的叫用方式是在表格式資料流程（TDS）封包中指定 ID = 3。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_cursorprepare prepared_handle OUTPUT, params , stmt , options  
    [ , scrollopt[ , ccopt]]  
```  
  
## <a name="arguments"></a>引數  
 *prepared_handle*  
 SQL Server 產生的備妥*控制碼*識別碼，會傳回整數值。  
  
> [!NOTE]  
>  *prepared_handle*接著會提供給 sp_cursorexecute 程式，以便開啟資料指標。 一旦建立控制代碼之後，在您登出或是透過 sp_cursorunprepare 程序明確將它移除之前，它都會存在。  
  
 *params*  
 識別參數化的陳述式。 變數的*params*定義會取代語句中的參數標記。 *params*是針對**Ntext**、 **Nchar**或**Nvarchar**輸入值呼叫的必要參數。 如果陳述式未參數化，則輸入 NULL 值。  
  
> [!NOTE]  
>  當*stmt*參數化且*scrollopt* PARAMETERIZED_STMT 值為 ON 時，請使用**Ntext**字串做為輸入值。  
  
 *把*  
 定義資料指標結果集。 *Stmt*參數是必要的，而且會呼叫**Ntext**、 **Nchar**或**Nvarchar**輸入值。  
  
> [!NOTE]  
>  指定*stmt*值的規則與 sp_cursoropen 相同，唯一的例外是*stmt*字串資料類型必須是**Ntext**。  
  
 *options*  
 傳回資料指標結果集資料行描述的選擇性參數。 *選項*需要下列**int**輸入值。  
  
|值|說明|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 捲動選項。 *scrollopt*是需要下列其中一個**int**輸入值的選擇性參數。  
  
|值|說明|  
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
  
 因為要求的值可能不適合*stmt*所定義的資料指標，所以這個參數會同時做為輸入和輸出。 在這類情況下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會指派適合的值。  
  
 *ccopt*  
 並行控制選項。 *ccopt*是需要下列其中一個**int**輸入值的選擇性參數。  
  
|值|說明|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS (之前稱為 LOCKCC)|  
|0x0004|**開放式**（先前稱為 OPTCC）|  
|0x0008|OPTIMISTIC (之前稱為 OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 如同*scrollpt*， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以從要求的值中指派不同的值。  
  
## <a name="remarks"></a>備註  
 RPC 狀態參數是下列其中一項：  
  
|值|說明|  
|-----------|-----------------|  
|0|Success|  
|0x0001|失敗|  
|1FF6|無法傳回中繼資料。<br /><br /> 注意：這是因為語句不會產生結果集。例如，它是 INSERT 或 DDL 語句。|  
  
## <a name="examples"></a>範例  
  以下是使用 sp_cursorprepare 和 sp_cursorexecute 的範例

```sql
declare @handle int , @p5 int, @p6 int
exec sp_cursorprepare @handle OUTPUT, 
    N'@dbid int', 
    N'select * from sys.databases where database_id < @dbid',
    1,
    @p5 output,
    @p6 output


declare @p1 int  
set @P1 = @handle 
declare @p2 int   
declare @p3 int  
declare @p4 int  
set @P6 = 4 
exec sp_cursorexecute @p1, @p2 OUTPUT, @p3 output , @p4 output, @p5 OUTPUT, @p6

exec sp_cursorfetch @P2

exec sp_cursorunprepare @handle
exec sp_cursorclose @p2
```
 
 當*stmt*參數化，且*scrollopt* PARAMETERIZED_STMT 值為 ON 時，字串的格式如下所示：  
  
 { * \< 本機變數名稱> * * \< 資料類型>* } [,.。。*n* ]  
  
## <a name="see-also"></a>另請參閱  
 [sp_cursorexecute &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [sp_cursoropen &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorunprepare &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursorunprepare-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
