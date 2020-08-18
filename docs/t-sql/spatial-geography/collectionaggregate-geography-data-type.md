---
description: CollectionAggregate (geometry 資料類型)
title: CollectionAggregate (geography 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CollectionAggregate method (geography)
ms.assetid: e49a644a-dbf2-46c3-98f5-4b3ec197e2ad
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: b49f1ab03be85c2c83caf50b548528ff36fd97b3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88360384"
---
# <a name="collectionaggregate-geography-data-type"></a>CollectionAggregate (geometry 資料類型)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

從 **geography** 物件集建立 **GeometryCollection** 執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
ConvexHullAggregate ( geography_operand )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *geography_operand*  
 這是 **geography** 型別資料表資料行，代表要列於 **GeometryCollection** 執行個體中的 **geography** 物件集。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
## <a name="exception"></a>例外狀況  
 輸入的值無效時，會擲回 `FormatException`。 請參閱 [STIsValid &#40;geography 資料型別&#41;](../../t-sql/spatial-geography/stisvalid-geography-data-type.md)  
  
## <a name="remarks"></a>備註  
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
  
  
