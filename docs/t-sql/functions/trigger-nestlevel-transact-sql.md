---
title: "TRIGGER_NESTLEVEL (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TRIGGER_NESTLEVEL
- TRIGGER_NESTLEVEL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- triggers [SQL Server], number executed
- number of triggers
- TRIGGER_NESTLEVEL function
ms.assetid: 6a33e74a-0cf9-4ae1-a1e4-4a137a3ea39d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0416b80079ac4c1dfb6dc10b507fd85800dd3a27
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="triggernestlevel-transact-sql"></a>TRIGGER_NESTLEVEL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回針對引發了觸發程序之陳述式而執行的觸發程序數目。 DML 和 DDL 觸發程序利用 TRIGGER_NESTLEVEL 來判斷目前的巢狀層級。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
TRIGGER_NESTLEVEL ( [ object_id ] , [ 'trigger_type' ] , [ 'trigger_event_category' ] )  
```  
  
## <a name="arguments"></a>引數  
 *object_id*  
 這是觸發程序的物件識別碼。 如果*object_id*指定，陳述式會傳回針對指定的觸發程序已執行的次數。 如果*object_id*未指定，陳述式會傳回所有觸發程序已執行的次數。  
  
 **'** *trigger_type* **'**  
 指定是否將 TRIGGER_NESTLEVEL 套用在 AFTER 觸發程序或 INSTEAD OF 觸發程序。 指定**AFTER** AFTER 觸發程序。 指定**IOT** INSTEAD OF 觸發程序。 如果*trigger_type*指定，則*trigger_event_category*也必須指定。  
  
 **'** *trigger_event_category* **'**  
 指定是否將 TRIGGER_NESTLEVEL 套用在 DML 或 DDL 觸發程序。 指定**DML** DML 觸發程序。 指定**DDL** DDL 觸發程序。 如果*trigger_event_category*指定，則*trigger_type*也必須指定。 請注意，只有**AFTER**可以使用指定**DDL**，因為 DDL 觸發程序只能是 AFTER 觸發程序。  
  
## <a name="remarks"></a>備註  
 當未指定任何參數時，TRIGGER_NESTLEVEL 會在呼叫堆疊上傳回觸發程序的總數。 其中包括它本身。 當觸發程序執行命令，造成引發另一個觸發程序或建立引發後續觸發程序時，可能會省略參數。  
  
 若要在特定觸發程序類型和事件類別目錄的呼叫堆疊上傳回觸發程序的總數，指定*object_id* = 0。  
  
 如果 TRIGGER_NESTLEVEL 在觸發程序之外執行，且有任何參數不是 NULL，它便會傳回 0。  
  
 當任何參數明確指定為 NULL 時，不論在觸發程序之內或之外使用 TRIGGER_NESTLEVEL，都會傳回 NULL 值。  
  
## <a name="examples"></a>範例  
  
### <a name="a-testing-the-nesting-level-of-a-specific-dml-trigger"></a>A. 測試特定 DML 觸發程序的巢狀層級  
  
```  
IF ( (SELECT TRIGGER_NESTLEVEL( OBJECT_ID('xyz') , 'AFTER' , 'DML' ) ) > 5 )  
   RAISERROR('Trigger xyz nested more than 5 levels.',16,-1)  
```  
  
### <a name="b-testing-the-nesting-level-of-a-specific-ddl-trigger"></a>B. 測試特定 DDL 觸發程序的巢狀層級  
  
```  
IF ( ( SELECT TRIGGER_NESTLEVEL ( ( SELECT object_id FROM sys.triggers  
WHERE name = 'abc' ), 'AFTER' , 'DDL' ) ) > 5 )  
   RAISERROR ('Trigger abc nested more than 5 levels.',16,-1)  
```  
  
### <a name="c-testing-the-nesting-level-of-all-triggers-executed"></a>C. 測試所有執行之觸發程序的巢狀層級  
  
```  
IF ( (SELECT trigger_nestlevel() ) > 5 )  
   RAISERROR  
      ('This statement nested over 5 levels of triggers.',16,-1)  
```  
  
## <a name="see-also"></a>請參閱＜  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
  
