---
title: Lat (geography 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Lat
- Lat_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Lat method
ms.assetid: 051d66bc-04de-4c58-861c-760dc5b859b5
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a932a0f29957d879edffa63c68880a20d81a8976
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="lat-geography-data-type"></a>Lat (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回 **geography** 執行個體的緯度屬性。  
  
## <a name="syntax"></a>語法  
  
```  
.Lat  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型：**float**  
  
 CLR 類型：**SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 在 OpenGIS 模型中，Lat 只會在由單一點組成的 **geography** 執行個體上定義。 如果 **geography** 執行個體包含多個單一點，此屬性將會傳回 NULL。 這個屬性是精確且唯讀的。  
  
## <a name="examples"></a>範例  
 下列範例會建立一個點，並傳回該點的緯度。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.Lat;  
```  
  
## <a name="see-also"></a>另請參閱  
 [地理例項上擴充的方法](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
