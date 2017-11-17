---
title: "ConvexHullAggregate (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ConvexHullAggregate_TSQL
- ConvexHullAggregate
dev_langs:
- TSQL
helpviewer_keywords:
- ConvexHullAggregate method (geography)
ms.assetid: 21784c66-2725-471b-9e2d-a8c2e3695197
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5a2f112e58838c754b946bdf3870fea31125a813
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="convexhullaggregate-geography-data-type"></a>ConvexHullAggregate (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回一組指定的凸殼**geography**物件。
  
## <a name="syntax"></a>語法  
  
```  
  
ConvexHullAggregate ( geography_operand )  
```  
  
## <a name="arguments"></a>引數  
 *geography_operand*  
 是**geography**類型資料表資料行，代表一組**geography**物件。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
## <a name="exception"></a>Exception  
 輸入的值無效時，會擲回 `FormatException`。 請參閱[STIsValid &#40; geography 資料類型 &#41;](../../t-sql/spatial-geography/stisvalid-geography-data-type.md)  
  
## <a name="remarks"></a>備註  
 方法會傳回**null**當輸入是空的或輸入具有不同的 Srid。 請參閱[空間參考識別碼 &#40;Srid &#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
 方法會忽略**null**輸入。  
  
> [!NOTE]  
>  方法會傳回**null**如果所有輸入的值為**null**。  
  
## <a name="examples"></a>範例  
 下列範例會傳回一組的凸殼**geography**物件。  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT geography::ConvexHullAggregate(SpatialLocation).ToString() AS SpatialLocation  
 FROM Person.Address  
 WHERE City LIKE ('Bothell')
 ```  
  
## <a name="see-also"></a>另請參閱  
 [擴充的靜態地理方法](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  

