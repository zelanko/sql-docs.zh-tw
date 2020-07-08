---
title: STOverlaps (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STOverlaps method (geography)
ms.assetid: 2babbb9c-59ef-4494-9e6b-528cf296cbd7
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a2d70a6af55587d87272c2317ea13e23f1d3a9ba
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85702321"
---
# <a name="stoverlaps-geography-data-type"></a>STOverlaps (geography 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  如果 **geography** 執行個體在空間上與另一個 **geography** 執行個體重疊，則傳回 1，否則傳回 0。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STOverlaps ( other_geography )  
```  
  
## <a name="arguments"></a>引數  
 *other_geography*  
 這是要與叫用 `STOverlaps()` 所在之執行個體相比較的另一個 **geography** 執行個體。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回類型：**SqlBoolean**  
  
## <a name="remarks"></a>備註  
 如果 **geography** 執行個體的空間參考識別碼 (SRID) 不相符，這個方法一律會傳回 null。  
  
## <a name="examples"></a>範例  
 下列範例使用 `STOverlaps()` 來測試兩個 **geography** 執行個體是否重疊。  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::Parse('POLYGON ((-120.533 46.566, -118.283 46.1, -122.3 47.45, -120.533 46.566))');  
SET @h = geography::Parse('CURVEPOLYGON (COMPOUNDCURVE (CIRCULARSTRING (-122.200928 47.454094, -122.810669 47.00648, -122.942505 46.687131, -121.14624 45.786679, -119.119263 46.183634), (-119.119263 46.183634, -119.273071 47.107523), CIRCULARSTRING (-119.273071 47.107523, -120.640869 47.569114, -122.200928 47.454094)))');  
SELECT @g.STOverlaps(@h);  
```  
  
  
