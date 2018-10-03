---
title: Parse (資料庫引擎) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Parse
- Parse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Parse [Database Engine]
ms.assetid: b37e28b6-6e2e-470a-945b-ce5252da743a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e808640ff9e408909ed38420bbb7620ddec34fc4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789016"
---
# <a name="parse-database-engine"></a>剖析 (Database Engine)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Parse 會將 **hierarchyid** 的標準字串表示法轉換成 **hierarchyid** 值。 將字串類型轉換成 **hierarchyid** 時，就會隱含呼叫 Parse。 其作用與 [ToString](../../t-sql/data-types/tostring-database-engine.md) 相反。 Parse() 是一種靜態方法。
  
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
*input*  
[!INCLUDE[tsql](../../includes/tsql-md.md)]：正在轉換的字元資料類型值。
  
CLR：正在評估的字串值。
  
## <a name="return-types"></a>傳回類型  
**SQL Server 傳回型別：hierarchyid**
  
**CLR 傳回型別：SqlHierarchyId**
  
## <a name="remarks"></a>Remarks  
若 Parse 收到一個值，而這個值不是 **hierarchyid** 的有效字串表示法，則會引發例外狀況。 例如，若 **char** 資料類型包含尾端空白，則會引發例外狀況。
  
## <a name="examples"></a>範例  
  
### <a name="a-converting-transact-sql-values-without-a-table"></a>A. 轉換 Transact-SQL 值而不使用資料表  
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
  
  
