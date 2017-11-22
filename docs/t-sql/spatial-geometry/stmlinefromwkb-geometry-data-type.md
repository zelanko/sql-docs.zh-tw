---
title: "STMLineFromWKB (geometry 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STMLineFromWKB (geometry Data Type)
- STMLineFromWKB_TSQL
dev_langs: TSQL
helpviewer_keywords: STMLineFromWKB (geometry Data Type)
ms.assetid: 00a8a8e7-11d6-47a0-b971-00e60f7877ce
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3d8b283da368ca98b851180e150ee125890984f3
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="stmlinefromwkb-geometry-data-type"></a>STMLineFromWKB (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回**geometryMultiLineString**從開放式地理空間協會 (OGC) 已知二進位 (well-known binary，WKB) 表示法的執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
STMLineFromWKB ( 'WKB_multilinestring' , SRID )  
```  
  
## <a name="arguments"></a>引數  
 *WKB_multilinestring*  
 是的 WKB 表示法**geometryMultiLineString**来傳回執行個體。 *WKB_multilinestring*是**varbinary （max)**運算式。  
  
 *SRID*  
 是**int**運算式，表示的空間參考識別碼 (SRID) 的**geometryMultiLineString**来傳回執行個體。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**幾何**  
  
 CLR 傳回類型： **SqlGeometry**  
  
 OGC 類型： **MultiLineString**  
  
## <a name="remarks"></a>備註  
 這個方法會擲回**FormatException**如果輸入格式不正確。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `STMLineFromWKB()` 建立 `geometry` 例項。  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STMLineFromWKB(0x0105000000020000000102000000020000000000000000005940000000000000594000000000000069400000000000006940010200000003000000000000000000084000000000000010400000000000001C40000000000000204000000000000024400000000000002440, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>請參閱＜  
 [OGC 靜態幾何方法](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

