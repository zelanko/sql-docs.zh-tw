---
title: STMPointFromText (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STMPointFromText (geometry Data Type)
- STMPointFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STMPointFromText (geometry Data Type)
ms.assetid: 37059074-5ee8-4f55-9414-1e958fd3adaf
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a12cc3f81e831639b7aa88770c5a57cbc3f35727
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38005670"
---
# <a name="stmpointfromtext-geometry-data-type"></a>STMPointFromText (geometry 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

從開放地理空間協會 (Open Geospatial Consortium，OGC) 的已知的文字 (Well-Known Text，WKT) 表示法傳回 **geometry** 執行個體，經由此執行個體夾帶的任何 Z (高度) 和 M (測量) 值來擴充。
  
## <a name="syntax"></a>語法  
  
```  
  
STMPointFromText ( 'multipoint_tagged_text', SRID )  
```  
  
## <a name="arguments"></a>引數  
 *multipoint_tagged_text*  
 這是要傳回之 **geometryMultiPoint** 執行個體的 WKT 表示法。 *multipoint_tagged_text* 是 **nvarchar(max)** 運算式。  
  
 *SRID*  
 這是 **int** 運算式，代表要傳回之 **geometryMultiPoint** 執行個體的空間參考識別碼 (SRID)。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geometry**  
  
 CLR 傳回類型：**SqlGeometry**  
  
 OGC 類型：**MultiPoint**  
  
## <a name="remarks"></a>Remarks  
 如果輸入的格式不正確，這個方法將會擲回 **FormatException**。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `STMPointFromText()` 建立 `geometry` 例項。  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STMPointFromText('MULTIPOINT ((100 100), (200 200))', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [OGC 靜態幾何方法](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

