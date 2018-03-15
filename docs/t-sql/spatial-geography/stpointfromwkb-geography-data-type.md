---
title: "STPointFromWKB (geography 資料型別) | Microsoft Docs"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STPointFromWKB_TSQL
- STPointFromWKB (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointFromWKB method
ms.assetid: b3b4e3bb-47bc-4621-99c4-c97aa60cdf8b
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2fe6278ce39724297be97eca1eefe03bcdce914e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="stpointfromwkb-geography-data-type"></a>STPointFromWKB (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

從開放地理空間協會 (OGC) 已知的二進位 (WKB) 表示法傳回 **geographyPoint** 執行個體。
  
## <a name="syntax"></a>語法  
  
```  
  
STPointFromWKB ( 'WKB_point' , SRID )  
```  
  
## <a name="arguments"></a>引數  
 *WKB_point*  
 這是您想要傳回之 **geographyPoint** 執行個體的 WKB 表示法。 *WKB_point* 是 **varbinary(max)** 運算式。  
  
 *SRID*  
 這是 **int** 運算式，表示要傳回之 **geographyPoint** 執行個體的空間參考識別碼 (SRID)。  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**geography**  
  
 CLR 傳回類型：**SqlGeography**  
  
 OGC 類型：**Point**  
  
## <a name="remarks"></a>Remarks  
 如果輸入的格式不正確，這個方法將會擲回 **FormatException**。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `STPointFromWKB()` 建立 `geography` 例項。  
  
```  
DECLARE @g geography;  
SET @g = geography::STPointFromWKB(0x010100000017D9CEF753D347407593180456965EC0, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>另請參閱  
 [OGC 靜態地理方法](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
