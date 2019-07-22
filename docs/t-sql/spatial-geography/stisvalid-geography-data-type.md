---
title: STIsValid (geography 資料型別) | Microsoft Docs
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
- STIsValid method (geography)
ms.assetid: 1bfe787f-ddf0-4fc7-af6a-570a58faab23
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 7c8b190e1678ff53d29e31dde55069739c2ce76f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079887"
---
# <a name="stisvalid-geography-data-type"></a>STIsValid (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  如果 **geography** 執行個體的格式正確，而且辨識為有效的地理物件 (根據它的開放地理空間協會 (OGC) 型別)，就會傳回 true。 如果 **geography** 執行個體的格式不正確，就會傳回 false。 這個方法是精確的。  
  
 這個 geography 資料類型方法可支援 **FullGlobe** 執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STIsValid ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回型別：**SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 可以叫用 [STGeometryType()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md) 來判斷 **geography** 執行個體的 OGC 型別。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只會產生有效的 **geography** 執行個體，但是允許儲存和擷取無效的執行個體。 可以使用 `MakeValid()` 方法來擷取表示無效執行個體之相同點組的有效執行個體。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `geography` 例項，並使用 `STIsValid()` 來測試此例項是否有效。  
  
```  
DECLARE @g geography = geography::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 4326);  
SELECT @g.STIsValid();  
DECLARE @g geography  
```  
  
## <a name="see-also"></a>另請參閱  
 [STGeometryType &#40;geography 資料型別&#41;](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md)   
 [MakeValid &#40;geography 資料類型&#41;](../../t-sql/spatial-geography/makevalid-geography-data-type.md)   
 [地理例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
