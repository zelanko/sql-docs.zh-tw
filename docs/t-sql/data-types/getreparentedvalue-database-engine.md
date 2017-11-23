---
title: "GetReparentedValue (Database Engine) |Microsoft 文件"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Reparent_TSQL
- Reparent
dev_langs: TSQL
helpviewer_keywords: Reparent [Database Engine]
ms.assetid: f47f8e25-08ef-498b-84f4-a317aca1f358
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e0b054e9651cce9a486d4acf9e997a601114e98a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="getreparentedvalue-database-engine"></a>GetReparentedValue (Database Engine)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回一個節點，其根路徑的路徑是路徑到*newRoot*，後面接著從路徑*oldRoot*至*這*。
  
## <a name="syntax"></a>語法  
  
```sql
-- Transact-SQL syntax  
node. GetReparentedValue ( oldRoot, newRoot )  
```  
  
```sql
-- CLR syntax  
SqlHierarchyId GetReparentedValue ( SqlHierarchyId oldRoot , SqlHierarchyId newRoot )  
```  
  
## <a name="arguments"></a>引數  
*oldRoot*  
A **hierarchyid**也就是代表即將修改之階層的層級的節點。
  
*newRoot*  
A **hierarchyid**表示的節點，將會取代*oldRoot*目前的節點，以便將節點移一節。
  
## <a name="return-types"></a>傳回類型  
**SQL Server 傳回類型： hierarchyid**
  
**CLR 傳回類型： SqlHierarchyId**
  
## <a name="remarks"></a>備註  
可用來移動的節點，藉以修改樹狀結構*oldRoot*至*newRoot*。 GetReparentedValue 可用來將階層的節點移至階層中的新位置。 **Hierarchyid**資料類型代表但不會強制的階層式結構。 使用者必須確保此 hierarchyid 已針對新位置適當地結構化。 上的唯一索引**hierarchyid**資料型別可協助防止重複的項目。 如需移動整個子樹的範例，請參閱[階層式資料 &#40;SQL Server &#41;](../../relational-databases/hierarchical-data-sql-server.md).
  
## <a name="examples"></a>範例  
  
### <a name="a-comparing-two-node-locations"></a>A. 比較兩個節點位置  
下列範例會顯示某個節點的目前 hierarchyid。 它也會顯示哪些**hierarchyid**節點的會是已進入節點變成的下階 **@NewParent** 節點。 它會使用 `ToString()` 方法來顯示階層式關聯性。
  
```sql
DECLARE @SubjectEmployee hierarchyid , @OldParent hierarchyid, @NewParent hierarchyid  
SELECT @SubjectEmployee = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\gail0' ;  
SELECT @OldParent = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\roberto0' ; -- who is /1/1/  
SELECT @NewParent = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\wanida0' ; -- who is /2/3/  
  
SELECT OrgNode.ToString() AS Current_OrgNode_AS_Text,   
(@SubjectEmployee. GetReparentedValue(@OldParent, @NewParent) ).ToString() AS Proposed_OrgNode_AS_Text,  
OrgNode AS Current_OrgNode,  
@SubjectEmployee. GetReparentedValue(@OldParent, @NewParent) AS Proposed_OrgNode,  
*  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode = @SubjectEmployee ;  
GO  
```  
  
### <a name="b-updating-a-node-to-a-new-location"></a>B. 將節點更新成新的位置  
下列範例會在 UPDATE 陳述式中使用 `GetReparentedValue()`，以便將某個節點從階層中的舊位置移至新位置：
  
```sql
DECLARE @SubjectEmployee hierarchyid , @OldParent hierarchyid, @NewParent hierarchyid  
SELECT @SubjectEmployee = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\gail0' ; -- Node /1/1/2/  
SELECT @OldParent = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\roberto0' ; -- Node /1/1/  
SELECT @NewParent = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\wanida0' ; -- Node /2/3/  
  
UPDATE HumanResources.EmployeeDemo  
SET OrgNode = @SubjectEmployee. GetReparentedValue(@OldParent, @NewParent)   
WHERE OrgNode = @SubjectEmployee ;  
  
SELECT OrgNode.ToString() AS Current_OrgNode_AS_Text,   
*  
FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\gail0' ; -- Now node /2/3/2/  
```  
  
### <a name="c-clr-example"></a>C. CLR 範例  
下列程式碼片段會呼叫 GetReparentedValue （） 方法：
  
```sql
this. GetReparentedValue(oldParent, newParent)  
```  
  
## <a name="see-also"></a>另請參閱
[Hierarchyid 資料類型方法參考](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[階層式資料 &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
