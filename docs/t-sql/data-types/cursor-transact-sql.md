---
title: cursor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- cursor data type
ms.assetid: fbea16ef-f2cc-4734-9149-ec2598fd3cca
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 083e748e9b0f01bb9c1e7386a7e35b345b1ffd5e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="cursor-transact-sql"></a>資料指標 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

參考資料指標的變數或預存程序 OUTPUT 參數的資料類型。
  
## <a name="remarks"></a>Remarks  
以下是可參考 **cursor** 資料類型之變數和參數的作業：
-   DECLARE *@local_variable* 和 SET *@local_variable* 陳述式。  
-   OPEN、FETCH、CLOSE 和 DEALLOCATE 資料指標陳述式。  
-   預存程序輸出參數。  
-   CURSOR_STATUS 函數。  
-   **sp_cursor_list**、**sp_describe_cursor**、**sp_describe_cursor_tables**，及 **sp_describe_cursor_columns** 系統預存程序。  
  
**sp_cursor_list** 和 **sp_describe_cursor** 的 **cursor_name** 輸出資料行會傳回 cursor 變數的名稱。
  
任何使用 **cursor** 資料類型建立的變數都可為 Null。
  
**cursor** 資料類型不能用於 CREATE TABLE 陳述式中的資料行。
  
## <a name="see-also"></a>另請參閱
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CURSOR_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-status-transact-sql.md)  
[資料類型轉換 &#40;資料庫引擎&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  
