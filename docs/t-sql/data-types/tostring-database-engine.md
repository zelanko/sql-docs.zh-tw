---
title: ToString (資料庫引擎) | Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ToString
- ToString_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ToString [Database Engine]
ms.assetid: 5fc11ca5-c26d-4518-9512-67aa0270f110
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b2bd8bdbe0c2de0baf598010cbec6604a3ff696f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37427207"
---
# <a name="tostring-database-engine"></a>ToString (Database Engine)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回具有 *this* 邏輯表示法的字串。 當從 **hierarchyid** 轉換成字串類型時，即會隱含地呼叫 ToString。 其行為是 [Parse &#40;Database Engine&#41;](../../t-sql/data-types/parse-database-engine.md) 的相反。
  
## <a name="syntax"></a>語法  
  
```sql
-- Transact-SQL syntax  
node.ToString  ( )   
-- This is functionally equivalent to the following syntax  
-- which implicitly calls ToString():  
CAST(node AS nvarchar(4000))  
```  
  
```sql
-- CLR syntax  
string ToString  ( )   
```  
  
## <a name="return-types"></a>傳回類型
**SQL Server 傳回型別：nvarchar(4000)**
  
**CLR 傳回型別：String**
  
## <a name="remarks"></a>Remarks  
傳回階層中的邏輯位置。 例如，`/2/1/` 表示下列檔案系統階層式結構中的第四個資料列 ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])：
  
```sql
/        C:\  
/1/      C:\Database Files  
/2/      C:\Program Files  
/2/1/    C:\Program Files\Microsoft SQL Server  
/2/2/    C:\Program Files\Microsoft Visual Studio  
/3/      C:\Windows  
```  
  
## <a name="examples"></a>範例  
  
### <a name="a-transact-sql-example-in-a-table"></a>A. 資料表中的 Transact-SQL 範例  
下列範例會以可讀性較佳的字串格式傳回 `OrgNode` 資料行和 **hierarchyid** 資料類型：
  
```sql
SELECT OrgNode,  
OrgNode.ToString() AS Node  
FROM HumanResources.EmployeeDemo  
ORDER BY OrgNode ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
OrgNode   Node  
0x        /  
0x58      /1/  
0x5AC0    /1/1/  
0x5B40    /1/2/  
0x5BC0    /1/3/  
0x5C20    /1/4/  
...  
```  
  
### <a name="b-converting-transact-sql-values-without-a-table"></a>B. 轉換 Transact-SQL 值而不使用資料表  
下列程式碼範例會使用 `ToString` 將 **hierarchyid** 值轉換成字串，並使用 `Parse` 將字串值轉換成 **hierarchyid**。
  
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
  
### <a name="c-clr-example"></a>C. CLR 範例  
下列程式碼片段會呼叫 ToString() 方法：
  
```sql
this.ToString()  
```  
  
## <a name="see-also"></a>另請參閱
[Hierarchyid 資料類型方法參考](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[階層式資料 &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
