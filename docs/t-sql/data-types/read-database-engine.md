---
title: Read (資料庫引擎) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Read_TSQL
- Read
dev_langs:
- TSQL
helpviewer_keywords:
- Read [Database Engine]
ms.assetid: f2b8207c-b69f-4327-a874-100b3a1f27d8
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 60575f2c5c5f1de4a7fa5b2531fb8431f13b4441
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="read-database-engine"></a>Read (Database Engine)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Read 會從傳入的 **BinaryReader** 讀取 **SqlHierarchyId** 的二進位表示法，並將 **SqlHierarchyId** 物件設為該值。 Read 無法使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 呼叫。 請改用 CAST 或 CONVERT。
  
## <a name="syntax"></a>語法  
  
```sql
void Read( BinaryReader r )   
```  
  
## <a name="arguments"></a>引數  
*r*  
 產生二進位資料流的 **BinaryReader** 物件，該資料流會對應到 **hierarchyid** 節點的二進位表示法。  
  
## <a name="return-types"></a>傳回型
 **CLR 傳回型別：void**  
  
## <a name="remarks"></a>Remarks  
 Read 不會驗證它的輸入。 若提供的二進位輸入無效，Read 便可能引發例外狀況。 或者它可能會成功，並產生無效的 **SqlHierarchyId** 物件，該物件的方法可提供無法預測的結果或引發例外狀況。  
  
 Read 只能在新建立的 **SqlHierarchyId** 物件上呼叫。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在需要的時候於內部使用 Read，例如將資料寫入 **hierarchyid** 資料行時。 在 **varbinary** 和 **hierarchyid** 之間進行轉換時，也會在內部呼叫 Read。  
  
## <a name="examples"></a>範例  
  
```sql
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
[Hierarchyid 資料類型方法參考](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  
