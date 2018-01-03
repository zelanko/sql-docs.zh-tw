---
title: "CHANGE_TRACKING_IS_COLUMN_IN_MASK (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/08/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHANGE_TRACKING_IS_COLUMN_IN_MASK_TSQL
- CHANGE_TRACKING_IS_COLUMN_IN_MASK
dev_langs: TSQL
helpviewer_keywords:
- change tracking [SQL Server], CHANGE_TRACKING_IS_COLUMN_IN_MASK
- CHANGE_TRACKING_IS_COLUMN_IN_MASK
ms.assetid: 649b370b-da54-4915-919d-1b597a39d505
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0ca1e489937aba92270fe73978f017c35b4fca99
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2018
---
# <a name="changetrackingiscolumninmask-transact-sql"></a>CHANGE_TRACKING_IS_COLUMN_IN_MASK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  解譯由 CHANGETABLE(CHANGES …) 函數傳回的 SYS_CHANGE_COLUMNS 值。 這可讓應用程式決定指定的資料行是否要包含在針對 SYS_CHANGE_COLUMNS 傳回的值中。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CHANGE_TRACKING_IS_COLUMN_IN_MASK ( column_id , change_columns )  
```  
  
## <a name="arguments"></a>引數  
 *column_id*  
 要經過檢查之資料行的識別碼。 可以使用來取得識別碼的資料行[COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md)函式。  
  
 *change_columns*  
 是的二進位資料之 SYS_CHANGE_COLUMNS 資料行[CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md)資料。  
  
## <a name="return-type"></a>傳回類型  
 **bit**  
  
## <a name="return-values"></a>傳回值  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK 會傳回下列值。  
  
|傳回值|描述|  
|------------------|-----------------|  
|0|指定的資料行不在*change_columns*清單。|  
|@shouldalert|指定資料行是在*change_columns*清單。|  
  
## <a name="remarks"></a>備註  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK 不會執行任何檢查來驗證*column_id*值，或*change_columns*參數是否從來源資料表中取得*column_id*取得。  
  
## <a name="examples"></a>範例  
 下列範例可判斷是否更新 `Salary` 資料表的 `Employees` 資料行。 `COLUMNPROPERTY`函式會傳回的資料行識別碼`Salary`資料行。 `@change_columns` 區域變數必須使用 CHANGETABLE 設定為查詢結果，做為資料來源。  
  
```sql  
SET @SalaryChanged = CHANGE_TRACKING_IS_COLUMN_IN_MASK  
    (COLUMNPROPERTY(OBJECT_ID('Employees'), 'Salary', 'ColumnId')  
    ,@change_columns);  
```  
  
## <a name="see-also"></a>請參閱  
 [變更追蹤函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [CHANGETABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [追蹤資料變更 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
