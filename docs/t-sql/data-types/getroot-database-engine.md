---
description: GetRoot (Database Engine)
title: GetRoot (資料庫引擎) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GetRoot
- GetRoot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetRoot [Database Engine]
ms.assetid: 240b70f1-eeda-44ab-b4bb-9e4af80fa7c0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5db6206cd555705ec5b167dc023f585293f45bf8
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91111229"
---
# <a name="getroot-database-engine"></a>GetRoot (Database Engine)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

傳回階層樹狀結構的根部。 GetRoot() 是一種靜態方法。
  
## <a name="syntax"></a>語法  
  
```syntaxsql
-- Transact-SQL syntax  
hierarchyid::GetRoot ( )   
```  
  
```syntaxsql
-- CLR syntax  
static SqlHierarchyId GetRoot ( )   
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>傳回型別  
**SQL Server 傳回型別：hierarchyid**
  
**CLR 傳回型別：SqlHierarchyId**
  
## <a name="remarks"></a>備註  
使用判斷階層樹狀結構中的根節點。
  
## <a name="examples"></a>範例  
  
### <a name="a-transact-sql-example"></a>A. Transact-SQL 範例  
下列範例會傳回階層樹狀結構的根部：
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode = hierarchyid::GetRoot()  
```  
  
### <a name="b-clr-example"></a>B. CLR 範例  
下列程式碼片段會呼叫 GetRoot() 方法：
  
```sql
SqlHierarchyId.GetRoot()  
```  
  
## <a name="see-also"></a>另請參閱
[Hierarchyid 資料類型方法參考](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[階層式資料 &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
