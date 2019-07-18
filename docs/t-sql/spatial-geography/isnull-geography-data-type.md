---
title: IsNull (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IsNull (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- IsNull method
ms.assetid: c031074f-bfda-4584-a3bf-4e7c324f237f
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: a780172818bd41fa3cff4804437b4d26ad8c95c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65937745"
---
# <a name="isnull-geography-data-type"></a>IsNull (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定 **geography** 執行個體是否為 Null 的屬性。 如果此執行個體為 Null 則會傳回 'TRUE'，如果此執行個體不是 Null 則傳回 0。  
  
## <a name="syntax"></a>語法  
  
```  
  
.IsNull  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型：**bit**  
  
 CLR 類型：**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 `IsNull` 可用來測試 **geography** 執行個體是否為 null。 這會產生令人混淆的結果，當此例項不是 Null 時傳回 0，但是如果此例項為 Null 則傳回 Null。  
  
 這個方法主要是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 基礎結構所使用；建議您使用 T-SQL 述詞 IS NULL 來測試 **geography** 執行個體是否為 Null。 如需 T-SQL 述詞 IS NULL 的詳細資訊，請參閱 [IS NULL &#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md)。  
  
## <a name="examples"></a>範例  
  
## <a name="see-also"></a>另請參閱  
 [地理例項上擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
