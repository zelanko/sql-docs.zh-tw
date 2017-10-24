---
title: "IsNull (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IsNull (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- IsNull method
ms.assetid: c031074f-bfda-4584-a3bf-4e7c324f237f
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9b9f65a3860b1b0d54231d3243fdfdf1902ae8ca
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="isnull-geography-data-type"></a>IsNull (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  此屬性，指定如果**geography**執行個體為 null。 如果此執行個體為 Null 則會傳回 'TRUE'，如果此執行個體不是 Null 則傳回 0。  
  
## <a name="syntax"></a>語法  
  
```  
  
.IsNull  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]類型：**位元**  
  
 CLR 型別： **SqlBoolean**  
  
## <a name="remarks"></a>備註  
 `IsNull`可以用來測試是否**geography**執行個體為 null。 這會產生令人混淆的結果，當此例項不是 Null 時傳回 0，但是如果此例項為 Null 則傳回 Null。  
  
 這個方法主要供[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]基礎結構，建議您使用 T-SQL 述詞 IS NULL 來測試是否**geography**執行個體為 null。 如需 T-SQL 述詞 IS NULL，請參閱[IS NULL &#40;TRANSACT-SQL &#41;](../../t-sql/queries/is-null-transact-sql.md).  
  
## <a name="examples"></a>範例  
  
## <a name="see-also"></a>另請參閱  
 [Geography 執行個體上的擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  

