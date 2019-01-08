---
title: CHANGE_TRACKING_IS_COLUMN_IN_MASK (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CHANGE_TRACKING_IS_COLUMN_IN_MASK_TSQL
- CHANGE_TRACKING_IS_COLUMN_IN_MASK
dev_langs:
- TSQL
helpviewer_keywords:
- change tracking [SQL Server], CHANGE_TRACKING_IS_COLUMN_IN_MASK
- CHANGE_TRACKING_IS_COLUMN_IN_MASK
ms.assetid: 649b370b-da54-4915-919d-1b597a39d505
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 534df29b5ad3422ed3290ce4037490f69f988832
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535746"
---
# <a name="changetrackingiscolumninmask-transact-sql"></a>CHANGE_TRACKING_IS_COLUMN_IN_MASK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  解譯 CHANGETABLE(CHANGES...) 函式所傳回的 SYS_CHANGE_COLUMNS 值。 這可讓應用程式決定指定的資料行是否要包含在針對 SYS_CHANGE_COLUMNS 傳回的值中。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CHANGE_TRACKING_IS_COLUMN_IN_MASK ( column_id , change_columns )  
```  
  
## <a name="arguments"></a>引數  
 *column_id*  
 要經過檢查之資料行的識別碼。 要取得 ID，請使用資料行[COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md)函式。  
  
 *change_columns*  
 二進位資料之 SYS_CHANGE_COLUMNS 資料行[CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md)資料。  
  
## <a name="return-type"></a>傳回類型  
 **bit**  
  
## <a name="return-values"></a>傳回值  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK 會傳回下列值。  
  
|傳回值|描述|  
|------------------|-----------------|  
|0|指定的資料行不是處於*change_columns*清單。|  
|1|指定的資料行正處於*change_columns*清單。|  
  
## <a name="remarks"></a>備註  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK 不會執行任何檢查來驗證*column_id*值，或*change_columns*參數已經從資料表取得*column_id*取得。  
  
## <a name="examples"></a>範例  
 下列範例可判斷是否更新 `Salary` 資料表的 `Employees` 資料行。 `COLUMNPROPERTY`函式會傳回的資料行識別碼`Salary`資料行。 `@change_columns` 區域變數必須使用 CHANGETABLE 設定為查詢結果，做為資料來源。  
  
```sql  
SET @SalaryChanged = CHANGE_TRACKING_IS_COLUMN_IN_MASK  
    (COLUMNPROPERTY(OBJECT_ID('Employees'), 'Salary', 'ColumnId')  
    ,@change_columns);  
```  
  
## <a name="see-also"></a>另請參閱  
 [變更追蹤函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [CHANGETABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [追蹤資料變更 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
