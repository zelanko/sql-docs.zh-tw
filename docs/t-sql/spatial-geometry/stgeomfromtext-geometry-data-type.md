---
title: STGeomFromText (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeomFromText (geometry Data Type)
- STGeomFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STGeomFromText (geometry Data Type)
ms.assetid: 20cace39-02e5-46c1-a9a5-841d04d0da16
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 3fe31cbf2e68d291edefcfbec013ecf9d73c99af
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65938889"
---
# <a name="stgeomfromtext-geometry-data-type"></a>STGeomFromText (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

從開放地理空間協會 (Open Geospatial Consortium，OGC) 的已知的文字 (Well-Known Text，WKT) 表示法傳回 **geometry** 執行個體，經由此執行個體夾帶的任何 Z (高度) 和 M (測量) 值來擴充。
  
## <a name="syntax"></a>語法  
  
```  
  
STGeomFromText ( 'geometry_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>引數  
 *geometry_tagged_text*  
 這是要傳回之 **geometry** 執行個體的 WKT 表示法。 *geometry_tagged_text* 是一個 **nvarchar(max)** 運算式。  
  
 *SRID*  
 這是 **int** 運算式，代表要傳回之 **geometry** 執行個體的空間參考識別碼 (SRID)。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geometry**  
  
 CLR 傳回型別：**SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 `STGeomFromText()` 所傳回之 **geometry** 執行個體的 OGC 類型會設定為對應的 WKT 輸入。  
  
 如果輸入的格式不正確，這個方法將會擲回 **FormatException**。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `STGeomFromText()` 建立 `geometry` 例項。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING (100 100, 20 180, 180 180)', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [OGC 靜態幾何方法](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

