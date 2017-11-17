---
title: "GetLevel (Database Engine) |Microsoft 文件"
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
- GetLevel
- GetLevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetLevel [Database Engine]
ms.assetid: 81577d7e-8ff6-4e73-b7f4-94c03d4921e7
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aac401d8fbe9546404f44f5fa2455f9e9c5dfe9d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="getlevel-database-engine"></a>GetLevel (Database Engine)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回一個整數，表示節點的深度*這*在樹狀目錄中。
  
## <a name="syntax"></a>語法  
  
```sql
-- Transact-SQL syntax  
node.GetLevel ( )   
```  
  
```sql
-- CLR syntax  
SqlInt16 GetLevel ( )   
```  
  
## <a name="return-types"></a>傳回類型  
**SQL Server 傳回類型： smallint**
  
**CLR 傳回類型： SqlInt16**
  
## <a name="remarks"></a>備註  
用來判斷一或多個節點的層級，或是將節點篩選至指定之層級的成員。 此階層的根節點為層級 0。
  
GetLevel 是廣度優先搜尋索引非常有用。 如需詳細資訊，請參閱[階層式資料 &#40;SQL Server &#41;](../../relational-databases/hierarchical-data-sql-server.md).
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-the-hierarchy-level-as-a-column"></a>A. 以資料行形式傳回階層層級  
下列範例會傳回的文字表示法**hierarchyid**，然後在階層層級和**EmpLevel**資料表中的所有資料列的資料行：
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo;  
```  
  
### <a name="b-returning-all-members-of-a-hierarchy-level"></a>B. 傳回階層層級的所有成員  
下列範例會傳回資料表中階層層級 2 的所有資料列：
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetLevel() = 2;  
```  
  
### <a name="c-returning-the-root-of-the-hierarchy"></a>C. 傳回階層的根節點  
下列範例會傳回此階層層級的根節點：
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetLevel() = 0;  
```  
  
### <a name="d-clr-example"></a>D. CLR 範例  
下列程式碼片段會呼叫 getlevel （） 方法：
  
```sql
this.GetLevel()  
```  
  
## <a name="see-also"></a>另請參閱
[Hierarchyid 資料類型方法參考](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[階層式資料 &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  

