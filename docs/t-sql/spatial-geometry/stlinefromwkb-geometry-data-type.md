---
title: "STLineFromWKB (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STLineFromWKB (geometry Data Type)
- STLineFromWKB_TSQL
dev_langs: TSQL
helpviewer_keywords: STLineFromWKB (geometry Data Type)
ms.assetid: e674c8c4-c67f-4fc1-9873-d9c2ed46c659
caps.latest.revision: "18"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 94ef2360ce423adb2edf085a160ee3b516c605e2
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="stlinefromwkb-geometry-data-type"></a>STLineFromWKB (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

傳回**geometryLineString**從開放式地理空間協會 (OGC) 已知二進位 (well-known binary，WKB) 表示法的執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
STLineFromWKB ( 'WKB_linestring' , SRID )  
```  
  
## <a name="arguments"></a>引數  
 *WKB_linestring*  
 是的 WKB 表示法**geometryLineString**您想要傳回的執行個體。 *WKB_linestring*是**varbinary （max)**運算式。  
  
 *SRID*  
 是**int**運算式，表示的空間參考識別碼 (SRID) 的**geometryLineString**您想要傳回的執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
 CLR 傳回類型： **SqlGeometry**  
  
 OGC 類型： **LineString**  
  
## <a name="remarks"></a>備註  
 這個方法會擲回**FormatException**如果輸入格式不正確。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `STLineFromWKB()` 建立 `geometry` 例項。  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STLineFromWKB(0x0102000000020000000000000000005940000000000000594000000000000069400000000000006940, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>請參閱＜  
 [OGC 靜態幾何方法](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

