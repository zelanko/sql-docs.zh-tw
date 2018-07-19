---
title: GetDescendant (資料庫引擎) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- GetDescendant_TSQL
- GetDescendant
dev_langs:
- TSQL
helpviewer_keywords:
- GetDescendant [Database Engine]
ms.assetid: f5f39596-033e-4243-acbc-caa188b45b03
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4fea2cf85ab38bfad67801b9ca3e5bfcd3f6297c
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37406947"
---
# <a name="getdescendant-database-engine"></a>GetDescendant (Database Engine)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回父系的子節點。
  
## <a name="syntax"></a>語法  
  
```sql
-- Transact-SQL syntax  
parent.GetDescendant ( child1 , child2 )   
```  
  
```sql
-- CLR syntax  
SqlHierarchyId GetDescendant ( SqlHierarchyId child1 , SqlHierarchyId child2 )   
```  
  
## <a name="arguments"></a>引數  
*child1*  
NULL 或目前節點子系的 **hierarchyid**。
  
*child2*  
NULL 或目前節點子系的 **hierarchyid**。
  
## <a name="return-types"></a>傳回類型  
**SQL Server 傳回型別：hierarchyid**
  
**CLR 傳回型別：SqlHierarchyId**
  
## <a name="remarks"></a>Remarks  
傳回父系之下階的一個子節點。
-   如果父系為 NULL，則會傳回 NULL。  
-   如果父系不是 NULL，而 child1 和 child2 都是 NULL，則會傳回父系的一個子系。  
-   如果父系和 child1 都不是 NULL，而 child2 是 NULL，則會傳回父系中大於 child1 的子系。  
-   如果父系和 child2 不是 NULL，而 child1 是 NULL，則會傳回父系中小於 child2 的子系。  
-   如果父系、child1 和 child2 都不是 NULL，則會傳回父系中大於 child1 且小於 child2 的子系。  
-   如果 child1 不是 NULL，也不是父系的子系，則會引發例外狀況。  
-   如果 child2 不是 NULL，也不是父系的子系，則會引發例外狀況。  
-   如果 child1 >= child2，則會引發例外狀況。  
  
GetDescendant 具確定性。 因此，當使用相同的輸入呼叫 GetDescendant 時，它一定會產生相同的輸出。 但是，所產生之子系的確實識別可能會取決於它與其他節點之間的關聯性而有所不同 (如範例 C 中所示範)。
  
## <a name="examples"></a>範例  
  
### <a name="a-inserting-a-row-as-the-least-descendant-node"></a>A. 插入資料列當做最不重要的下階節點  
當雇用新的員工時，向 `/3/1/` 節點上的現有員工報告。 執行下列程式碼來插入新的資料列，其方式是使用 GetDescendant 方法而不包含引數，將新的資料列節點指定為 `/3/1/1/`：
  
```sql
DECLARE @Manager hierarchyid;   
SET @Manager = CAST('/3/1/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(NULL, NULL),  
'adventure-works\FirstNewEmployee', 'Application Intern', '3/11/07') ;  
```  
  
### <a name="b-inserting-a-row-as-a-greater-descendant-node"></a>B. 插入資料列當做比較重要的下階節點  
雇用另一個新的員工，向範例 A 的相同經理報告。執行下列程式碼來插入新的資料列，其方式是使用 GetDescendant 方法 (使用 child1 引數)，以指定新資料列的節點將會遵循範例 A 中的節點，變成 `/3/1/2/`：
  
```sql
DECLARE @Manager hierarchyid, @Child1 hierarchyid;  
  
SET @Manager = CAST('/3/1/' AS hierarchyid);  
SET @Child1 = CAST('/3/1/1/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(@Child1, NULL),  
'adventure-works\SecondNewEmployee', 'Application Intern', '3/11/07') ;  
```  
  
### <a name="c-inserting-a-row-between-two-existing-nodes"></a>C. 在兩個現有的節點中插入資料列  
雇用第三個員工，向範例 A 的相同經理報告。這個範例會將新的資料列插入大於範例 A 中 `FirstNewEmployee` 且小於範例 B 中 `SecondNewEmployee` 的節點。請使用 GetDescendant 方法來執行下列程式碼。 同時使用 child1 引數和 child2 引數指定新資料列的節點將會變成 `/3/1/1.1/` 節點：
  
```sql
DECLARE @Manager hierarchyid, @Child1 hierarchyid, @Child2 hierarchyid;  
  
SET @Manager = CAST('/3/1/' AS hierarchyid);  
SET @Child1 = CAST('/3/1/1/' AS hierarchyid);  
SET @Child2 = CAST('/3/1/2/' AS hierarchyid);  
  
INSERT HumanResources.EmployeeDemo (OrgNode, LoginID, Title, HireDate)  
VALUES  
(@Manager.GetDescendant(@Child1, @Child2),  
'adventure-works\ThirdNewEmployee', 'Application Intern', '3/11/07') ;  
  
```  
  
完成範例 A、B 和 C 以後，新增至資料表的節點將會是具有下列 **hierarchyid** 值的對等項：
  
`/3/1/1/`
  
`/3/1/1.1/`
  
`/3/1/2/`
  
節點 `/3/1/1.1/` 大於節點 `/3/1/1/`，但是兩者位於階層中的同一層。
  
### <a name="d-scalar-examples"></a>D. 純量範例  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援任何 **hierarchyid** 節點的任意插入及刪除。 藉由使用 GetDescendant()，可能會在任兩個 **hierarchyid** 節點之間產生節點。 使用 `GetDescendant` 執行下列程式碼來產生範例節點：
  
```sql
DECLARE @h hierarchyid = hierarchyid::GetRoot();  
DECLARE @c hierarchyid = @h.GetDescendant(NULL, NULL);  
SELECT @c.ToString();  
DECLARE @c2 hierarchyid = @h.GetDescendant(@c, NULL);  
SELECT @c2.ToString();  
SET @c2 = @h.GetDescendant(@c, @c2);  
SELECT @c2.ToString();  
SET @c = @h.GetDescendant(@c, @c2);  
SELECT @c.ToString();  
SET @c2 = @h.GetDescendant(@c, @c2);  
SELECT @c2.ToString();  
```  
  
### <a name="e-clr-example"></a>E. CLR 範例  
下列程式碼片段會呼叫 `GetDescendant()` 方法：
  
```sql
SqlHierarchyId parent, child1, child2;  
parent = SqlHierarchyId.GetRoot();  
child1 = parent.GetDescendant(SqlHierarchyId.Null, SqlHierarchyId.Null);  
child2 = parent.GetDescendant(child1, SqlHierarchyId.Null);  
Console.Write(parent.GetDescendant(child1, child2).ToString());  
```  
  
## <a name="see-also"></a>另請參閱
[Hierarchyid 資料類型方法參考](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[階層式資料 &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
