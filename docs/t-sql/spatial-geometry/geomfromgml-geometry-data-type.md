---
title: GeomFromGml (geometry 資料型別) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- GeomFromGML_TSQL
- GeomFromGML
dev_langs:
- TSQL
helpviewer_keywords:
- GeomFromGML (geometry Data Type)
ms.assetid: a3f2c84b-a49f-4ce3-ba25-b903fb0c99b4
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c846f048c639926f8f79d7573c1f64a5d04f89ae
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="geomfromgml-geometry-data-type"></a>GeomFromGml (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

在提供了地理標記語言 (GML) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 子集中的表示法時，建構 **geometry** 執行個體。
  
如需有關地理標記語言 (GML) 的詳細資訊，請參閱以下開放式地理空間協會規格：
  
[OGC 規格，地理標記語言](http://go.microsoft.com/fwlink/?LinkId=93629) \(英文\)
  
## <a name="syntax"></a>語法  
  
```  
  
GeomFromGml ( GML_input, SRID )  
```  
  
## <a name="arguments"></a>引數  
 *GML_input*  
 這是 XML 輸入，GML 將會從此輸入傳回值。  
  
 *SRID*  
 這是 **int** 運算式，代表要傳回之 **geometry** 執行個體的空間參考識別碼 (SRID)。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geometry**  
  
 CLR 傳回類型：**SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 如果輸入的格式不正確，這個方法將會擲回 **FormatException**。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `GeomFromGml()` 建立 `geometry` 例項。  
  
```  
DECLARE @g geometry;  
DECLARE @x xml;  
SET @x = '<LineString xmlns="http://www.opengis.net/gml"> <posList>100 100 20 180 180 180</posList> </LineString>';  
SET @g = geometry::GeomFromGml(@x, 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [擴充的靜態幾何方法](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

