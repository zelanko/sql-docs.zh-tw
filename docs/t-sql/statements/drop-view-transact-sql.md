---
title: "卸除檢視 (TRANSACT-SQL) |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_VIEW_TSQL
- DROP VIEW
dev_langs:
- TSQL
helpviewer_keywords:
- dropping views
- DROP VIEW statement
- deleting views
- indexed views [SQL Server], removing
- views [SQL Server], removing
- removing views
ms.assetid: 03cea355-e39c-46e1-b7db-8832038669dd
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8dedeff21f56659d0cc55eef2d133a1ecbe0f63e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="drop-view-transact-sql"></a>DROP VIEW (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  從目前資料庫移除一或多份檢視。 您可以針對索引檢視來執行 DROP VIEW。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
DROP VIEW [ IF EXISTS ] [ schema_name . ] view_name [ ...,n ] [ ; ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP VIEW [ schema_name . ] view_name   
[;]  
```  
  
## <a name="arguments"></a>引數  
 *如果存在*  
 **適用於**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[新版](http://go.microsoft.com/fwlink/p/?LinkId=299658)， [!INCLUDE[sssds](../../includes/sssds-md.md)])。 |  
  
 只有當它已經存在有條件地卸除檢視。  
  
 *schema_name*  
 這是檢視所屬的結構描述名稱。  
  
 *view_name*  
 這是要移除的檢視名稱。  
  
## <a name="remarks"></a>備註  
 當您卸除檢視時，也會從系統目錄中刪除檢視的定義和檢視的其他相關資訊。 檢視的所有權限也都會刪除。  
  
 在利用 DROP TABLE 來卸除的資料表中，您必須利用 DROP VIEW 來明確卸除任何檢視。  
  
 當針對索引檢視來執行時，DROP VIEW 會自動卸除檢視的所有索引。 若要顯示在檢視上的所有索引，請使用[sp_helpindex](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)。  
  
 當查詢檢視時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會檢查確定陳述式所參考的所有資料庫物件都存在、在陳述式的內容中有效，而且修改資料陳述式未違反任何資料完整性規則。 檢查失敗會傳回錯誤訊息。 檢查成功會將動作轉換成針對基礎資料表的動作。 如果基礎資料表或檢視在最初建立檢視之後有了改變，卸除再重建檢視可能有用。  
  
 如需判斷相依性的特定檢視的詳細資訊，請參閱[sys.sql_dependencies &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md).  
  
 如需檢視的檢視表文字的詳細資訊，請參閱[sp_helptext &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 需要**控制項**檢視的權限**ALTER**上檢視或中的成員資格所包含的結構描述的權限**db_ddladmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
  
### <a name="a-drop-a-view"></a>A. 卸除檢視  
 下列範例會移除 `Reorder` 檢視。  
  
```  
DROP VIEW dbo.Reorder ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/alter-view-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [使用 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/use-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
 

