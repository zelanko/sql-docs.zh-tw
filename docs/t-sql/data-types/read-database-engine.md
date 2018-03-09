---
title: "讀取 (Database Engine) |Microsoft 文件"
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
- Read_TSQL
- Read
dev_langs:
- TSQL
helpviewer_keywords:
- Read [Database Engine]
ms.assetid: f2b8207c-b69f-4327-a874-100b3a1f27d8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 72ebda7a9bd00b44983d29db2ef433c9f7d43f94
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="read-database-engine"></a>Read (Database Engine)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

讀取可讀取的二進位表示法**SqlHierarchyId**從傳入的**BinaryReader**並設定**SqlHierarchyId**該值的物件。 無法藉由呼叫讀取[!INCLUDE[tsql](../../includes/tsql-md.md)]。 請改用 CAST 或 CONVERT。
  
## <a name="syntax"></a>語法  
  
```sql
void Read( BinaryReader r )   
```  
  
## <a name="arguments"></a>引數  
*r*  
 **BinaryReader**產生對應至以二進位形式的二進位資料流的物件**hierarchyid**節點。  
  
## <a name="return-types"></a>傳回型別
 **CLR 傳回類型： void**  
  
## <a name="remarks"></a>備註  
 讀取並不會驗證其輸入。 如果指定無效的二進位輸入，讀取可能會引發例外狀況。 或者，它可能會成功，並產生無效**SqlHierarchyId**物件，其方法可以產生無法預期的結果或引發例外狀況。  
  
 讀取只能呼叫上新建立**SqlHierarchyId**物件。  
  
 讀取會在內部使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會在必要時，例如當寫入資料至**hierarchyid**資料行。 讀取為也在內部呼叫之間進行轉換時**varbinary**和**hierarchyid**。  
  
## <a name="examples"></a>範例  
  
```sql
Byte[] encoding = new byte[] { 0x58 };  
MemoryStream stream = new MemoryStream(encoding, false /*not writable*/);  
BinaryReader br = new BinaryReader(stream);  
SqlHierarchyId hid = new SqlHierarchyId();  
hid.Read(br);   
```  
  
## <a name="see-also"></a>請參閱＜  
[寫入 &#40; Database engine&#41;](../../t-sql/data-types/write-database-engine.md)  
[ToString &#40; Database engine&#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Hierarchyid 資料類型方法參考](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  
