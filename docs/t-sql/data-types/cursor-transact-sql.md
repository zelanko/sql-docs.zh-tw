---
title: "資料指標 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- cursor data type
ms.assetid: fbea16ef-f2cc-4734-9149-ec2598fd3cca
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4b0b96a3bc147f51102fa10f2dff96b7f1761759
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="cursor-transact-sql"></a>資料指標 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

參考資料指標的變數或預存程序 OUTPUT 參數的資料類型。
  
## <a name="remarks"></a>備註  
可以參考變數和參數的作業**游標**資料類型為：
-   DECLARE  *@local_variable* 和設定 *@local_variable* 陳述式。  
-   OPEN、FETCH、CLOSE 和 DEALLOCATE 資料指標陳述式。  
-   預存程序輸出參數。  
-   CURSOR_STATUS 函數。  
-   **Sp_cursor_list**， **sp_describe_cursor**， **sp_describe_cursor_tables**，和**sp_describe_cursor_columns**系統預存程序。  
  
**Cursor_name**輸出資料行**sp_cursor_list**和**sp_describe_cursor**傳回資料指標變數的名稱。
  
使用建立的任何變數**游標**資料型別是可為 null。
  
**游標**資料類型不能用於 CREATE TABLE 陳述式中的資料行。
  
## <a name="see-also"></a>另請參閱
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CURSOR_STATUS &#40;TRANSACT-SQL &#41;](../../t-sql/functions/cursor-status-transact-sql.md)  
[資料類型轉換 &#40; Database Engine &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[宣告資料指標 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  

