---
title: GetRoot (資料庫引擎) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
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
manager: craigg
ms.openlocfilehash: ba02bf9f5bf5511b9e334921170e493c8cc84ebc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47598946"
---
# <a name="getroot-database-engine"></a>GetRoot (Database Engine)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回階層樹狀結構的根部。 GetRoot() 是一種靜態方法。
  
## <a name="syntax"></a>語法  
  
```sql
-- Transact-SQL syntax  
hierarchyid::GetRoot ( )   
```  
  
```sql
-- CLR syntax  
static SqlHierarchyId GetRoot ( )   
```  
  
## <a name="return-types"></a>傳回類型  
**SQL Server 傳回型別：hierarchyid**
  
**CLR 傳回型別：SqlHierarchyId**
  
## <a name="remarks"></a>Remarks  
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
[Hierarchyid 資料類型方法參考](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[階層式資料 &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
