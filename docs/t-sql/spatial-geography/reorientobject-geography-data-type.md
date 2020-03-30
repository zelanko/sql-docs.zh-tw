---
title: ReorientObject (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ReorientObject
- ReorientObject_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ReorientObject method (geography)
ms.assetid: e2a1a4f1-211b-4e82-abed-03fc7140a83c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 9c4660fa212a85f3bba5812d6cc990f9c02c5539
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68101747"
---
# <a name="reorientobject-geography-data-type"></a>ReorientObject (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

傳回具有可交替使用之內部區域與外部區域的 **geography** 執行個體。  
  
這個 **geography** 資料類型方法可支援 **FullGlobe** 執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.ReorientObject (geography)  
```  
  
## <a name="arguments"></a>引數  
_地理位置_  
這是叫用 **所在的另一個**geography`ReorientObject()` 執行個體。  
  
## <a name="return-value"></a>傳回值  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
CLR 傳回類型：**SqlGeography**  
  
## <a name="remarks"></a>備註  
這個方法會變更 **GeometryCollection** 中所有 **Polygons** 的環方向，但不會移除或變更指定集合中的任何 **Points**或 **Linestrings**。  
  
如果您將 **GeometryCollection** 傳遞至這個方法，則集合中每個執行個體的方向都會重新調整，但不會重新調整整個集合的方向。  
  
## <a name="examples"></a>範例  
  
```  
DECLARE @R GEOGRAPHY = GEOGRAPHY::Parse('Polygon((-10 -10, -10 10, 10 10, 10 -10, -10 -10))');  
SELECT @R.ReorientObject().STAsText();  
--Result: POLYGON ((10 10, -10 10, -10 -10, 10 -10, 10 10))  
```  
  
## <a name="see-also"></a>另請參閱  
[地理例項上擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
