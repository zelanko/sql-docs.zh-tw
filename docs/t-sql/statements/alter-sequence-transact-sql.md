---
title: "ALTER SEQUENCE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/08/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_SEQUENCE_TSQL
- ALTER SEQUENCE
dev_langs:
- TSQL
helpviewer_keywords:
- sequence number object, altering
- ALTER SEQUENCE statement
ms.assetid: decc0760-029e-4baf-96c9-4a64073df1c2
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 66960ed0ae27cb7ecbe2d39d0e30d1ec12dcc3cb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="alter-sequence-transact-sql"></a>ALTER SEQUENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  修改現有順序物件的引數。 如果建立序列時**快取**選項時，改變順序會重新建立快取。  
  
 建立順序物件使用[CREATE SEQUENCE](../../t-sql/statements/create-sequence-transact-sql.md)陳述式。 順序是整數值，可以是任何傳回整數的資料類型。 資料類型無法透過 ALTER SEQUENCE 陳述式來變更。 若要變更資料類型，請卸除並重新建立順序物件。  
  
 順序是使用者定義的結構描述繫結物件，該物件會根據規格產生數值序列。 藉由呼叫 NEXT VALUE FOR 函數，從順序產生新值。 您可以使用 **sp_sequence_get_range** 一次取得多個序號。 資訊和案例，使用 CREATE SEQUENCE、 **sp_sequence_get_range**，和 NEXT VALUE FOR 函式，請參閱[序號](../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
ALTER SEQUENCE [schema_name. ] sequence_name  
    [ RESTART [ WITH <constant> ] ]  
    [ INCREMENT BY <constant> ]  
    [ { MINVALUE <constant> } | { NO MINVALUE } ]  
    [ { MAXVALUE <constant> } | { NO MAXVALUE } ]  
    [ CYCLE | { NO CYCLE } ]  
    [ { CACHE [ <constant> ] } | { NO CACHE } ]  
    [ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *sequence_name*  
 指定資料庫中順序的唯一識別名稱。 型別是**sysname**。  
  
 重新啟動 [WITH\<常數 >]  
 順序物件會傳回的下一個值。 如果提供的話，RESTART WITH 值必須是小於或等於順序物件最大值，而且大於或等於最小值的整數。 如果省略 WITH 值，順序編號會依據原始 CREATE SEQUENCE 選項重新啟動。  
  
 遞增的\<常數 >  
 每次呼叫 NEXT VALUE FOR 函數時，用來遞增順序物件基底值的值 (如果是負數則遞減)。 如果增量是負值，則會遞減順序物件，否則會遞增。 增量不能為 0。  
  
 [MINVALUE\<常數 > |沒有 MINVALUE]  
 指定順序物件的界限。 如果指定 NO MINVALUE，則使用順序資料類型的最小可能值。  
  
 [MAXVALUE\<常數 > |沒有 MAXVALUE  
 指定順序物件的界限。 如果指定 NO MAXVALUE，則使用順序資料類型的最大可能值。  
  
 [ CYCLE | NO CYCLE ]  
 這個屬性指定當超出其最小值或最大值時，順序物件應該從最小值 (或是遞減順序物件的最大值) 重新啟動，還是擲回例外狀況。  
  
> [!NOTE]  
>  在循環之後，下一個值是順序的最小值或最大值，而不是 START VALUE。  
  
 [快取 [\<常數 >] |無快取]  
 藉由減少產生的值保存至系統資料表時所需的 IO 數目，對使用順序物件的應用程式提升效能。  
  
 快取行為的詳細資訊，請參閱[CREATE SEQUENCE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-sequence-transact-sql.md).  
  
## <a name="remarks"></a>備註  
 如需有關如何建立順序以及如何管理順序快取資訊，請參閱[CREATE SEQUENCE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-sequence-transact-sql.md).  
  
 遞增順序的 MINVALUE 和遞減順序的 MAXVALUE 值不可改變成不允許順序的 START WITH 值。 若要將遞增順序的 MINVALUE 變更為大於 START WITH 值的數字或將遞減順序的 MAXVALUE 變更為小於 START WITH 的數字，請在最小值和最大值範圍內的所需落點包含 RESTART WITH 引數來重新啟動順序。  
  
## <a name="metadata"></a>中繼資料  
 如需有關順序的詳細資訊，請查詢 [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md)。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 需要**ALTER**序列上的權限或**ALTER**結構描述權限。 若要授與**ALTER**權限的順序，請使用**ALTER ON OBJECT**格式如下：  
  
```  
GRANT ALTER ON OBJECT::Test.TinySeq TO [AdventureWorks\Larry]  
```  
  
 順序物件的擁有權可以傳送使用**ALTER AUTHORIZATION**陳述式。  
  
### <a name="audit"></a>稽核  
 若要稽核**ALTER SEQUENCE**，監視**SEQUENCE<**。  
  
## <a name="examples"></a>範例  
 如需建立順序和使用的範例**NEXT VALUE FOR**函數產生序號，請參閱[序號](../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
### <a name="a-altering-a-sequence"></a>A. 改變順序  
 下列範例會建立名為 Test 的結構描述和名為 q 使用序列**int**具備範圍從 0 到 255 之間的資料類型。 順序開頭為 125，而且每次產生數字時會遞增 25。 因為順序設定為循環，所以當值超過最大值 200 時，順序會從最小值 100 重新啟動。  
  
```  
CREATE SCHEMA Test ;  
GO  
  
CREATE SEQUENCE Test.TestSeq  
    AS int   
    START WITH 125  
    INCREMENT BY 25  
    MINVALUE 100  
    MAXVALUE 200  
    CYCLE  
    CACHE 3  
;  
GO  
```  
  
 下列範例會改變 q 順序範圍從 0 到 255 之間。 順序會從 100 重新啟動編號數列，而且每次產生數字時遞增 50。  
  
```  
ALTER SEQUENCE Test. TestSeq  
    RESTART WITH 100  
    INCREMENT BY 50  
    MINVALUE 50  
    MAXVALUE 200  
    NO CYCLE  
    NO CACHE  
;  
GO  
```  
  
 因為順序不會循環， **NEXT VALUE FOR**當順序超過 200 時，函數會造成錯誤。  
  
### <a name="b-restarting-a-sequence"></a>B. 重新啟動順序  
 下列範例會建立名為 CountBy1 的順序。 順序會使用預設值。  
  
```  
CREATE SEQUENCE Test.CountBy1 ;  
```  
  
 為了產生順序值，擁有者接著執行下列陳述式：  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1  
```  
  
 傳回值-9223372036854775808 是最低的可能值**bigint**資料型別。 擁有者發現他想要開頭為 1 的順序，但未指出**START WITH**他建立順序時的子句。 為了更正這個錯誤，擁有者執行下列陳述式。  
  
```  
ALTER SEQUENCE Test.CountBy1 RESTART WITH 1 ;  
```  
  
 擁有者接著重新執行下列陳述式產生序號。  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1;  
```  
  
 數字現在為 1，如預期。  
  
 使用 NO CYCLE 預設值，因此作業在產生 9,223,372,036,854,775,807 數字之後，它會停止建立 CountBy1 順序。 順序物件的後續呼叫會傳回錯誤 11728。 下列陳述式會將順序物件變更為循環，並設定 20 的快取。  
  
```  
ALTER SEQUENCE Test.CountBy1  
    CYCLE  
    CACHE 20 ;  
  
```  
  
 現在當順序物件達到 9,223,372,036,854,775,807 時，它會循環，而且下一個數字在循環之後將會是資料類型的最小值 -9,223,372,036,854,775,808。  
  
 擁有者發現**bigint**資料型別就會使用 8 個位元組，每次使用時。 **Int**使用 4 個位元組的資料類型已足夠。 但是順序物件的資料類型無法改變。 若要變更為**int**資料類型，擁有者必須卸除順序物件並重新建立具有正確的資料類型的物件。  
  
## <a name="see-also"></a>請參閱＜  
 [建立順序 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [卸除順序 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [下一個值 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [序號](../../relational-databases/sequence-numbers/sequence-numbers.md)   
 [sp_sequence_get_range &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md)  
  
  
