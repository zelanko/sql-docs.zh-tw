---
title: "IsDescendantOf (Database Engine) |Microsoft 文件"
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
- IsDescendant_TSQL
- IsDescendant
dev_langs:
- TSQL
helpviewer_keywords:
- IsDescendantOf [Database Engine]
ms.assetid: edc80444-b697-410f-9419-0f63c9b5618d
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0f8ff83344e577e5479e21316a3c043d6ef4f702
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="isdescendantof-database-engine"></a>IsDescendantOf (Database Engine)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回 true，否則*這*是父代的子代。
  
## <a name="syntax"></a>語法  
  
```sql
-- Transact-SQL syntax  
child. IsDescendantOf ( parent )  
```  
  
```sql
-- CLR syntax  
SqlHierarchyId IsDescendantOf (SqlHierarchyId parent )  
```  
  
## <a name="arguments"></a>引數  
*父代*  
**Hierarchyid** IsDescendantOf 測試應該執行的節點。
  
## <a name="return-types"></a>傳回類型  
**SQL Server 傳回的型別： 位元**
  
**CLR 傳回類型： SqlBoolean**
  
## <a name="remarks"></a>備註  
針對位於父系之子樹中的所有節點傳回 true，而針對所有其他節點傳回 false。
  
父系會被視為自己的下階。
  
## <a name="examples"></a>範例  
  
### <a name="a-using-isdescendantof-in-a-where-clause"></a>A. 在 WHERE 子句中使用 IsDescendantOf  
下列範例會傳回經理以及向經理提出報告的員工：
  
```sql
DECLARE @Manager hierarchyid  
SELECT @Manager = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\dylan0'  
  
SELECT * FROM HumanResources.EmployeeDemo  
WHERE OrgNode.IsDescendantOf(@Manager) = 1  
```  
  
### <a name="b-using-isdescendantof-to-evaluate-a-relationship"></a>B. 使用 IsDescendantOf 來評估關聯性  
下列程式碼會宣告並填入三個變數。 然後，它會評估階層式關聯性，並且根據比較，傳回兩個列印結果的其中之一：
  
```sql
DECLARE @Manager hierarchyid, @Employee hierarchyid, @LoginID nvarchar(256)  
SELECT @Manager = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\terri0' ;  
  
SELECT @Employee = OrgNode, @LoginID = LoginID FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\rob0'  
  
IF @Employee.IsDescendantOf(@Manager) = 1  
   BEGIN  
    PRINT 'LoginID ' + @LoginID + ' is a subordinate of the selected Manager.'  
   END  
ELSE  
   BEGIN  
    PRINT 'LoginID ' + @LoginID + ' is not a subordinate of the selected Manager.' ;  
   END  
```  
  
### <a name="c-calling-a-common-language-runtime-method"></a>C. 呼叫 Common Language Runtime 方法  
下列程式碼片段會呼叫 `IsDescendantOf()` 方法。
  
```sql
this.IsDescendantOf(Parent)  
```  
  
## <a name="see-also"></a>另請參閱
[Hierarchyid 資料類型方法參考](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[階層式資料 &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

