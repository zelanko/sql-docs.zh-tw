---
title: "剖析 (Database Engine) |Microsoft 文件"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Parse
- Parse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Parse [Database Engine]
ms.assetid: b37e28b6-6e2e-470a-945b-ce5252da743a
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 027940c7575f3c7901cd8668879064ff375d9986
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="parse-database-engine"></a>剖析 (Database Engine)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

剖析的標準字串表示轉換**hierarchyid**至**hierarchyid**值。 從字串類型轉換時隱含地呼叫 parse **hierarchyid** ，就會發生。 做為相反[ToString](../../t-sql/data-types/tostring-database-engine.md)。 Parse() 是靜態方法。
  
## <a name="syntax"></a>語法  
  
```sql
-- Transact-SQL syntax  
hierarchyid::Parse ( input )  
-- This is functionally equivalent to the following syntax   
-- which implicitly calls Parse():  
CAST ( input AS hierarchyid )  
```  
  
```sql
-- CLR syntax  
static SqlHierarchyId Parse ( SqlString input )   
```  
  
## <a name="arguments"></a>引數  
*輸入*  
[!INCLUDE[tsql](../../includes/tsql-md.md)]：正在轉換的字元資料類型值。
  
CLR：正在評估的字串值。
  
## <a name="return-types"></a>傳回類型  
**SQL Server 傳回類型： hierarchyid**
  
**CLR 傳回類型： SqlHierarchyId**
  
## <a name="remarks"></a>備註  
如果剖析接收到的值不是有效的字串表示， **hierarchyid**，例外狀況。 例如，如果**char**資料類型包含尾端空白，會引發例外狀況。
  
## <a name="examples"></a>範例  
  
### <a name="a-converting-transact-sql-values-without-a-table"></a>A. 轉換 Transact-SQL 值而不使用資料表  
下列程式碼範例使用`ToString`轉換**hierarchyid**值到一個字串，並`Parse`將字串值轉換成**hierarchyid**。
  
```sql
DECLARE @StringValue AS nvarchar(4000), @hierarchyidValue AS hierarchyid  
SET @StringValue = '/1/1/3/'  
SET @hierarchyidValue = 0x5ADE  
  
SELECT hierarchyid::Parse(@StringValue) AS hierarchyidRepresentation,  
@hierarchyidValue.ToString() AS StringRepresentation ;
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
hierarchyidRepresentation    StringRepresentation
-------------------------    -----------------------
0x5ADE                       /1/1/3/
```
  
### <a name="b-clr-example"></a>B. CLR 範例  
下列程式碼片段會呼叫 Parse() 方法：
  
```sql
string input = “/1/2/”;  
SqlHierarchyId.Parse(input);  
```  
  
## <a name="see-also"></a>另請參閱
[Hierarchyid 資料類型方法參考](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[階層式資料 &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

