---
description: GetLevel (Database Engine)
title: GetLevel (資料庫引擎) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GetLevel
- GetLevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetLevel [Database Engine]
ms.assetid: 81577d7e-8ff6-4e73-b7f4-94c03d4921e7
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f0aa604a88902dc8bfba522556f11b267fa1e184
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037161"
---
# <a name="getlevel-database-engine"></a>GetLevel (Database Engine)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

傳回代表樹狀結構中 *this* 節點深度的整數。
  
## <a name="syntax"></a>語法  
  
```syntaxsql
-- Transact-SQL syntax  
node.GetLevel ( )   
```  
  
```syntaxsql
-- CLR syntax  
SqlInt16 GetLevel ( )   
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>傳回型別  
**SQL Server 傳回型別：smallint**
  
**CLR 傳回型別：SqlInt16**
  
## <a name="remarks"></a>備註  
用來判斷一或多個節點的層級，或是將節點篩選至指定之層級的成員。 此階層的根節點為層級 0。
  
GetLevel 對於廣度優先的搜尋索引很有用。 如需詳細資訊，請參閱[階層式資料 &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)。
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-the-hierarchy-level-as-a-column"></a>A. 以資料行形式傳回階層層級  
下列範例會傳回 **hierarchyid** 的文字表示法，並針對所有資料表中的資料列將階層層級以 **EmpLevel** 資料行傳回：
  
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
下列程式碼片段會呼叫 GetLevel() 方法：
  
```sql
this.GetLevel()  
```  
  
## <a name="see-also"></a>另請參閱
[Hierarchyid 資料類型方法參考](./hierarchyid-data-type-method-reference.md)  
[階層式資料 &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
