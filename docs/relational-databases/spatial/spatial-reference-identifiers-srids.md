---
title: 空間參考識別碼 (SRID) | Microsoft Docs
ms.date: 03/29/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Spatial Reference Identifiers (SRIDs)
- geodetic spatial data [SQL Server], identifiers
- SRID
ms.assetid: 0612658a-7d1b-4178-bdc2-42b914ea31a7
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c7d95c1c3b1c8f578a80601b4996e1c6bd9dd63c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85666544"
---
# <a name="spatial-reference-identifiers-srids"></a>空間參考識別碼 (SRID)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  每一個空間執行個體都有空間參考識別碼 (SRID)， 此 SRID 會對應到空間參考系統，此系統是以用於扁平表面對應或圓形表面對應的特定橢圓體為根據。  
  
 空間資料行可包含具有不同 SRID 的物件。 但是，當針對資料使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 空間資料方法來執行作業時，只能使用具有相同 SRID 的空間執行個體。 衍生自兩個空間資料執行個體的任何空間方法結果只有在這兩個執行個體具有相同的 SRID (根據用來判斷執行個體座標的相同度量、資料和投射單位) 時，才是有效的。 最常見的 SRID 度量單位是公尺或平方公尺。  
  
 如果兩個空間執行個體沒有相同的 SRID，則執行個體上所用之 **geometry** 或 **geography** 資料類型方法的結果將會傳回 NULL。 例如，如果要讓下列述詞傳回非 NULL 的結果，兩個 **geometry** 執行個體 ( `geometry1` 和 `geometry2`) 必須有相同的 SRID：  
  
 `geometry1.STIntersects(geometry2) = 1`  
  
> [!NOTE]  
>  空間參考識別系統是由 [歐洲石油探勘組織 (EPSG)](https://go.microsoft.com/fwlink/?LinkId=99349) 標準所定義，這是為了地圖製作、探勘和測地資料儲存所開發的一套標準。 這項標準的擁有者為石油生產者 (OGP) 探勘和定位委員會 (Oil and Gas Producers (OGP) Surveying and Positioning Committee)。  
  
## <a name="see-also"></a>另請參閱  
 [空間資料類型概觀](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
