---
description: STContains (geography 資料類型)
title: STContains (geography 資料類型) | Microsoft Docs
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
- STContains method (geography)
ms.assetid: b10e8f0a-2926-449a-82ea-be42543420ca
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: d3e9b03eac0107792b9b0cdb59359f5ad70b5474
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459073"
---
# <a name="stcontains--geography-data-type"></a>STContains (geography 資料類型)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  指定呼叫 **geography** 執行個體是否在空間上包含傳遞給方法的 **geography** 執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STContains ( other_geography )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *other_geography*  
 這是要與叫用 `STContains()` 所在之執行個體相比較的另一個 **geography** 執行個體。  
  
## <a name="return-types"></a>傳回型別  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回類型：**bit**  
  
 CLR 傳回類型：**SqlBoolean**  
  
## <a name="remarks"></a>備註  
 如果呼叫 **geography** 執行個體在空間上包含傳遞給方法的 **geography** 執行個體，則傳回 1，否則傳回 0。 如果兩個 **geography** 執行個體的 SRID 並不相同，則傳回 **null**。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `STContains()` 來測試兩個 `geography` 執行個體，看看第一個執行個體是否包含第二個執行個體。  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::Parse('CURVEPOLYGON (COMPOUNDCURVE (CIRCULARSTRING (-122.200928 47.454094, -122.810669 47.00648, -122.942505 46.687131, -121.14624 45.786679, -119.119263 46.183634), (-119.119263 46.183634, -119.273071 47.107523, -120.640869 47.569114, -122.200928 47.454094)))');  
SET @h = geography::Parse('POINT(-121.703796 46.893985)');  
```  
  
 `SELECT @g.STContains(@h);`  
  
  
