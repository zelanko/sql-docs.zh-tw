---
description: IsDescendantOf (Database Engine)
title: IsDescendantOf (資料庫引擎) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IsDescendant_TSQL
- IsDescendant
dev_langs:
- TSQL
helpviewer_keywords:
- IsDescendantOf [Database Engine]
ms.assetid: edc80444-b697-410f-9419-0f63c9b5618d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b6d9d75083472b347a7cf78641aeb1bbe202dae2
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91111270"
---
# <a name="isdescendantof-database-engine"></a>IsDescendantOf (Database Engine)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

若 *this* 為父代的子系，便會傳回 true。
  
## <a name="syntax"></a>語法  
  
```syntaxsql
-- Transact-SQL syntax  
child. IsDescendantOf ( parent )  
```  
  
```syntaxsql
-- CLR syntax  
SqlHierarchyId IsDescendantOf (SqlHierarchyId parent )  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
*parent*  
應執行 IsDescendantOf 測試的 **hierarchyid** 節點。
  
## <a name="return-types"></a>傳回型別  
**SQL Server 傳回型別：bit**
  
**CLR 傳回型別：SqlBoolean**
  
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
[Hierarchyid 資料類型方法參考](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[階層式資料 &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
