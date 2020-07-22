---
title: STPointN (geometry 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STPointN_TSQL
- STPointN (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointN (geometry Data Type)
ms.assetid: 8f0bb3b7-5cd9-42c2-b9f8-f04628653bd0
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: eced8c5e3c7d42abf8974af1efc9202bd30bed27
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554901"
---
# <a name="stpointn-geometry-data-type"></a>STPointN (geometry 資料類型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

傳回 **geometry** 執行個體中的指定點。
  
## <a name="syntax"></a>語法  
  
```  
  
.STPointN ( expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *expression*  
 這是 1 與 **geometry** 執行個體中點數之間的 **int** 運算式。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geometry**  
  
 CLR 傳回類型：**SqlGeometry**  
  
 開放地理空間協會 (OGC) 類型：**Point**  
  
## <a name="remarks"></a>備註  
 如果 **geometry** 執行個體是使用者所建立的，`STPointN()` 會傳回 *expression* 所指定的點，其方式是依據原先輸入點的順序來排序這些點。  
  
 如果 **geometry** 執行個體是系統所建構的，`STPointN()` 會傳回 *expression* 所指定的點，其方式是依據將輸出這些點的順序來排序所有點：先依據幾何，再依據幾何內的環形 (如果適用)，然後再依據環形內的點。 這個順序具決定性。  
  
 如果使用小於 1 的值來呼叫此方法，它會擲回 **ArgumentOutOfRangeException**。  
  
 如果使用大於例項中點數的值來呼叫此方法，它會傳回 Null。  
  
## <a name="examples"></a>範例  
 下列範例會建立 `LineString` 例項，並使用 `STPointN()` 來擷取例項描述中的第二個點。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [幾何例項上的 OGC 方法](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

