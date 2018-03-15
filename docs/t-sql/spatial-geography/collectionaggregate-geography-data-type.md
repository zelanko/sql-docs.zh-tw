---
title: "CollectionAggregate (geography 資料型別) | Microsoft Docs"
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
dev_langs:
- TSQL
helpviewer_keywords:
- CollectionAggregate method (geography)
ms.assetid: e49a644a-dbf2-46c3-98f5-4b3ec197e2ad
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4c697a43ac6b79fd137da968ce5f01e49e60c105
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="collectionaggregate-geography-data-type"></a>CollectionAggregate (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

從 **geography** 物件集建立 **GeometryCollection** 執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
ConvexHullAggregate ( geography_operand )  
```  
  
## <a name="arguments"></a>引數  
 *geography_operand*  
 這是 **geography** 型別資料表資料行，代表要列於 **GeometryCollection** 執行個體中的 **geography** 物件集。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
## <a name="exception"></a>例外狀況  
 輸入的值無效時，會擲回 `FormatException`。 請參閱 [STIsValid &#40;geography 資料型別&#41;](../../t-sql/spatial-geography/stisvalid-geography-data-type.md)  
  
## <a name="remarks"></a>Remarks  
 當輸入是空的或輸入具有不同 SRID 時，此方法會傳回 **null**。 請參閱[空間參考識別碼 &#40;SRIDs&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
 此方法會忽略 **null** 輸入。  
  
> [!NOTE]  
>  如果所有輸入的值都為 **null**，此方法就會傳回 **null**。  
  
## <a name="examples"></a>範例  
 下列範例會傳回包含 **geography** 物件集的 `GeometryCollection` 執行個體。  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT geography::CollectionAggregate(SpatialLocation).ToString() AS SpatialLocation  
 FROM Person.Address  
 WHERE City LIKE ('Bothell')
 ```  
  
## <a name="see-also"></a>另請參閱  
 [擴充的靜態地理方法](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
