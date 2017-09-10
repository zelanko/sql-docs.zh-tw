---
title: "MakeValid (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- MakeValid method (geography)
ms.assetid: f67038e3-4f62-4465-994e-e95ac27d8ada
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ca7928d73b20bfa024466cc580b1958c250c9d8e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="makevalid-geography-data-type"></a>MakeValid (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  將轉換**geography**無效，無法轉換為有效的執行個體**geography**具有有效開放式地理空間協會 (OGC) 類型的執行個體。  
  
 如果輸入的物件會傳回 False，d，如`MakeValid()`轉換是無效的有效執行個體的執行個體。  
  
 這個 geography 資料類型方法可支援**FullGlobe**執行個體或大於半球的空間執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.MakeValid ()  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
## <a name="remarks"></a>備註  
 這個方法可變更的類型**geography**執行個體。 此外，點**geography**執行個體可能會稍微。 來自某些方法，例如 NumPoint() 結果可能會變更。  
  
 無效的空間執行個體與赤道交集，而且具有 EnvelopeAngle() = 180 **FullGlobe**會傳回執行個體。 `MakeValid()` **Geography**資料類型方法可讓最佳嘗試傳回有效的執行個體，但不是保證結果準確或精確。  
  
> [!NOTE]  
>  無效的物件可以儲存在資料庫中。 在無效執行個體上執行的方法 （如哪些 d 這些執行個體傳回 False） 為方法來檢查有效性或允許匯出： d、 makevalid （）、 stastext （）、 STAsBinary()、 tostring （）、 AsTextZM() 和 AsGml()。  
  
 這個方法並不精確。  
  
## <a name="examples"></a>範例  
 第一個範例會建立與自己重疊的無效 `LineString` 例項，並使用 `STIsValid()` 來確認它是無效的例項。 `STIsValid()` 會針對無效的例項傳回 0 的值。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(0 2, 1 1, 1 0, 1 1, 2 2)', 4326);  
SELECT @g.STIsValid();  
```  
  
 第二個範例會使用 `MakeValid()` 讓此例項變成有效及測試看看此例項是否真正有效。 `STIsValid()` 會針對有效的例項傳回 1 的值。  
  
```  
SET @g = @g.MakeValid();  
SELECT @g.STIsValid();  
```  
  
 第三個範例會確認此例項已做了哪些變更而成為有效的例項。  
  
```  
SELECT @g.ToString();  
```  
  
 在此範例中，當選取 `LineString` 例項時，值會當做有效的 `MultiLineString` 例項傳回。  
  
```  
MULTILINESTRING ((0 2, 1 1, 2 2), (1 1, 1 0))  
```  
  
## <a name="see-also"></a>另請參閱  
 [STIsValid &#40;geometry 資料類型&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [Geography 執行個體上的擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
