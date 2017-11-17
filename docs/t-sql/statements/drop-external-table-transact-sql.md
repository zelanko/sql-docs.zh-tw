---
title: "卸除外部資料表 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 02a6a236-0756-4570-abfa-6f677a7df042
caps.latest.revision: 12
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 7cf14c5782a5cdc876b04600447892932f9e9921
ms.contentlocale: zh-tw
ms.lasthandoff: 10/24/2017

---
# <a name="drop-external-table-transact-sql"></a>卸除外部資料表 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  移除從 PolyBase 外部資料表。 這不會刪除外部的資料。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
DROP EXTERNAL TABLE [ database_name . [schema_name ] . | schema_name . ] table_name   
[;]  
```  
  

## <a name="arguments"></a>引數  
 [ *database_name* 。 [*schema_name*]。 | *schema_name* 。 ] *table_name*  
 要移除之外部資料表的一至三部分名稱。 資料表名稱可以選擇性地包含結構描述，或資料庫和結構描述。  
  
## <a name="permissions"></a>Permissions  
  
-   需要**ALTER**資料表所屬結構描述權限。  
  
## <a name="general-remarks"></a>一般備註  
 卸除的外部資料表移除所有資料表與相關的中繼資料。 它不會刪除外部的資料。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-basic-syntax"></a>A. 使用基本語法  
  
```  
DROP EXTERNAL TABLE SalesPerson;  
DROP EXTERNAL TABLE dbo.SalesPerson;  
DROP EXTERNAL TABLE EasternDivision.dbo.SalesPerson;  
```  
  
### <a name="b-dropping-an-external-table-from-the-current-database"></a>B. 從目前資料庫中卸除的外部資料表  
 下列範例會移除`ProductVendor1`資料表、 資料、 索引和任何相依的檢視，從目前的資料庫。  
  
```  
DROP EXTERNAL TABLE ProductVendor1;  
```  
  
### <a name="c-dropping-a-table-from-another-database"></a>C. 從另一個資料庫中卸除的資料表  
 下列範例會卸除 `EasternDivision` 資料庫中的 `SalesPerson` 資料表。  
  
```  
DROP EXTERNAL TABLE EasternDivision.dbo.SalesPerson;  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE EXTERNAL TABLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  


