---
title: Read (資料庫引擎) | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Read_TSQL
- Read
dev_langs:
- TSQL
helpviewer_keywords:
- Read [Database Engine]
ms.assetid: f2b8207c-b69f-4327-a874-100b3a1f27d8
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 89739f7e53ddccfc95cb9e84311f1ed18e147de6
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552583"
---
# <a name="read-database-engine-by-using-csharp"></a>使用 CSharp 讀取 (資料庫引擎)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Read 會從傳入的 **BinaryReader** 讀取 **SqlHierarchyId** 的二進位表示法，並將 **SqlHierarchyId** 物件設為該值。 Read 無法使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 呼叫。 請改用 CAST 或 CONVERT。
  
## <a name="syntax"></a>語法  

<!--
This is not T-SQL, despite the ```sql colorizer specified.
Neither should this be ```syntaxsql.
Rather, this is C# (or C# syntax).  Same for the later code blocks.
I am making this fix now, from ```sql to ```cs, on 2020/04/16.  GeneMi.
-->

```csharp
void Read( BinaryReader r )   
```  

## <a name="arguments"></a>引數
*r*  
 產生二進位資料流的 **BinaryReader** 物件，該資料流會對應到 **hierarchyid** 節點的二進位表示法。  
  
## <a name="return-types"></a>傳回類型
 **CLR 傳回型別：void**  
  
## <a name="remarks"></a>備註  
 Read 不會驗證它的輸入。 若提供的二進位輸入無效，Read 便可能引發例外狀況。 或者它可能會成功，並產生無效的 **SqlHierarchyId** 物件，該物件的方法可提供無法預測的結果或引發例外狀況。  
  
 Read 只能在新建立的 **SqlHierarchyId** 物件上呼叫。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在需要的時候於內部使用 Read，例如將資料寫入 **hierarchyid** 資料行時。 在 **varbinary** 和 **hierarchyid** 之間進行轉換時，也會在內部呼叫 Read。  
  
## <a name="examples"></a>範例  
  
```csharp
Byte[] encoding = new byte[] { 0x58 };  
MemoryStream stream = new MemoryStream(encoding, false /*not writable*/);  
BinaryReader br = new BinaryReader(stream);  
SqlHierarchyId hid = new SqlHierarchyId();  
hid.Read(br);   
```  
  
## <a name="see-also"></a>另請參閱  
[Write &#40;資料庫引擎&#41;](../../t-sql/data-types/write-database-engine.md)  
[ToString &#40;資料庫引擎&#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Hierarchyid 資料類型方法參考](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  
