---
description: STGeometryN (geography 資料類型)
title: STGeometryN (geography 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeometryN (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryN method
ms.assetid: 53755f69-cd50-475b-b3b8-a1a9157cf03a
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 812a5e63f21de77028c1f00a08f1819c5a07be13
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88445240"
---
# <a name="stgeometryn-geography-data-type"></a>STGeometryN (geography 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  傳回 **GeometryCollection** 中指定的 **geography** 元素或是它的其中一個子類型。 當在 **GeometryCollection** 的子類型 (例如 **MultiPoint** 或 **MultiLineString**) 上使用 STGeometryN() 時，如果使用 N = 1 呼叫，這個方法會傳回 **geography** 執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STGeometryN ( expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *expression*  
 這是介於 1 和 **GeometryCollection** 內的 **geography** 執行個體數目之間的 **int** 運算式。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
 CLR 傳回類型：**SqlGeography**  
  
## <a name="remarks"></a>備註  
 如果參數大於 [STNumGeometries()](../../t-sql/spatial-geography/stnumgeometries-geography-data-type.md) 的結果，這個方法會傳回 null；如果 *expression* 參數小於 1，將會擲回 **ArgumentOutOfRangeException**。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `MultiPoint``geography` 執行個體，並使用 `STGeometryN()` 來尋找 **GeometryCollection** 的第二個 `geography` 執行個體。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STGeometryN(2).ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理位置例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
