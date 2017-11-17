---
title: "寫入 (Database Engine) |Microsoft 文件"
ms.custom: 
ms.date: 7/23/2017
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
- Write_TSQL
- Write
dev_langs:
- TSQL
helpviewer_keywords:
- Write [Database Engine]
ms.assetid: 7c554334-d2d9-4eae-a4ae-097aa4020e1a
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 60707b57671c2ad607bd85b0fedececccd478038
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="write-database-engine"></a>Write (Database Engine)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

寫入寫出的二進位表示法**SqlHierarchyId**要傳入的**BinaryWriter**。 無法使用呼叫寫入[!INCLUDE[tsql](../../includes/tsql-md.md)]。 請改用 CAST 或 CONVERT。
  
## <a name="syntax"></a>語法  
  
```sql
void Write( BinaryWriter w )   
```  
  
## <a name="arguments"></a>引數  
*w*  
A **BinaryWriter**的目標物件的二進位表示這個**hierarchyid**節點會寫出。
  
## <a name="return-types"></a>傳回類型  
**CLR 傳回類型： void**
  
## <a name="remarks"></a>備註  
寫入在內部使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會在必要時，例如載入資料時**hierarchyid**資料行。 寫入為也在內部呼叫之間進行轉換時**hierarchyid**和**varbinary**。
  
## <a name="examples"></a>範例  
  
```sql
MemoryStream stream = new MemoryStream();  
BinaryWriter bw = new BinaryWriter(stream);  
hid.Write(bw);  
byte[] encoding = stream.ToArray();  
  
```  
  
## <a name="see-also"></a>另請參閱
[讀取 &#40; Database Engine &#41;](../../t-sql/data-types/read-database-engine.md)  
[ToString &#40; Database engine&#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Hierarchyid 資料類型方法參考](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  

