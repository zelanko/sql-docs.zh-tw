---
description: TRIGGER_NESTLEVEL (Transact-SQL)
title: TRIGGER_NESTLEVEL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 86554070c90b2c946e79359b561da324abbf700a
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "91379533"
---
# <a name="trigger_nestlevel-transact-sql"></a>TRIGGER_NESTLEVEL (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  傳回針對引發了觸發程序之陳述式而執行的觸發程序數目。 DML 和 DDL 觸發程序利用 TRIGGER_NESTLEVEL 來判斷目前的巢狀層級。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
TRIGGER_NESTLEVEL ( [ object_id ] , [ 'trigger_type' ] , [ 'trigger_event_category' ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 object_id  
 這是觸發程序的物件識別碼。 若指定 *object_id*，則會傳回針對陳述式執行指定觸發程序的次數。 如果未指定 *object_id*，則會傳回針對陳述式而執行之所有觸發程序的次數。  
  
 **'** *trigger_type* **'**  
 指定是否將 TRIGGER_NESTLEVEL 套用在 AFTER 觸發程序或 INSTEAD OF 觸發程序。 指定 **AFTER** 表示 AFTER 觸發程序。 指定 **IOT** 表示 INSTEAD OF 觸發程序。 若指定 *trigger_type*，則也必須同時指定 *trigger_event_category*。  
  
 **'** *trigger_event_category* **'**  
 指定是否將 TRIGGER_NESTLEVEL 套用在 DML 或 DDL 觸發程序。 為 DML 觸發程序指定 **DML**。 為 DDL 觸發程序指定 **DDL**。 若指定 *trigger_event_category*，則也必須同時指定 *trigger_type*。 請注意，只有 **AFTER** 可以指定 **DDL**，因為 DDL 觸發程序只能是 AFTER 觸發程序。  
  
## <a name="remarks"></a>備註  
 當未指定任何參數時，TRIGGER_NESTLEVEL 會在呼叫堆疊上傳回觸發程序的總數。 其中包括它本身。 當觸發程序執行命令，造成引發另一個觸發程序或建立引發後續觸發程序時，可能會省略參數。  
  
 若要在特定觸發程序類型和事件類別的呼叫堆疊上，傳回觸發程序的總數，請指定 *object_id* = 0。  
  
 如果 TRIGGER_NESTLEVEL 在觸發程序之外執行，且有任何參數不是 NULL，它便會傳回 0。  
  
 當任何參數明確指定為 NULL 時，不論在觸發程序之內或之外使用 TRIGGER_NESTLEVEL，都會傳回 NULL 值。  
  
## <a name="examples"></a>範例  
  
### <a name="a-testing-the-nesting-level-of-a-specific-dml-trigger"></a>A. 測試特定 DML 觸發程序的巢狀層級  
  
```sql
IF ( (SELECT TRIGGER_NESTLEVEL( OBJECT_ID('xyz') , 'AFTER' , 'DML' ) ) > 5 )  
   RAISERROR('Trigger xyz nested more than 5 levels.',16,-1)  
```  
  
### <a name="b-testing-the-nesting-level-of-a-specific-ddl-trigger"></a>B. 測試特定 DDL 觸發程序的巢狀層級  
  
```sql
IF ( ( SELECT TRIGGER_NESTLEVEL ( ( SELECT object_id FROM sys.triggers  
WHERE name = 'abc' ), 'AFTER' , 'DDL' ) ) > 5 )  
   RAISERROR ('Trigger abc nested more than 5 levels.',16,-1)  
```  
  
### <a name="c-testing-the-nesting-level-of-all-triggers-executed"></a>C. 測試所有執行之觸發程序的巢狀層級  
  
```sql
IF ( (SELECT trigger_nestlevel() ) > 5 )  
   RAISERROR  
      ('This statement nested over 5 levels of triggers.',16,-1)  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
  
