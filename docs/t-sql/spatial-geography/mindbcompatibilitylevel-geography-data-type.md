---
title: "MinDbCompatibilityLevel (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MinDbCompatibilityLevel
- MinDbCompatibilityLevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MinDbCompatibilityLevel method (geography)
ms.assetid: a9e44748-4a9e-4179-abc4-7631597be5a7
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6c95aafc0278834c6108b99dd67908958fb47b17
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="mindbcompatibilitylevel-geography-data-type"></a>MinDbCompatibilityLevel (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  傳回可辨識的最低資料庫相容性**geography**資料型別。  
  
## <a name="syntax"></a>語法  
  
```  
  
. MinDbCompatibilityLevel ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別： **int**  
  
 CLR 傳回類型： **int**  
  
## <a name="remarks"></a>備註  
 在變更資料庫的相容性層級之前，請先使用 `MinDbCompatibilityLevel()` 測試空間物件的相容性。 無效的**geography**類型會傳回 110。  
  
## <a name="examples"></a>範例  
  
### <a name="a-testing-circularstring-type-for-compatibility-with-compatibility-level-110"></a>A. 使用相容性層級 110 測試 CircularString 類型的相容性  
 下列範例會測試 `CircularString` 執行個體與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的相容性：  
  
```  
DECLARE @g geometry = 'CIRCULARSTRING(-120.533 46.566, -118.283 46.1, -122.3 47.45)';  
IF @g.MinDbCompatibilityLevel() <= 110  
BEGIN  
    SELECT @g.ToString();  
END  
  
```  
  
### <a name="b-testing-linestring-type-for-compatibility-with-compatibility-level-100"></a>B. 使用相容性層級 100 測試 LineString 類型的相容性  
 下列範例會測試 `LineString` 執行個體與 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 的相容性：  
  
```  
DECLARE @g geometry = 'LINESTRING(-120.533 46.566, -118.283 46.1, -122.3 47.45)';  
IF @g.MinDbCompatibilityLevel() <= 100  
BEGIN  
    SELECT @g.ToString();  
END  
  
```  
  
### <a name="c-testing-the-value-of-a-geography-instance-for-compatibility"></a>C. 測試地理位置執行個體值的相容性  
 下列範例示範兩個 `geography` 執行個體的相容性層級。 一個小於半球，另一個大於半球：  
  
```  
DECLARE @g geography = geography::Parse('POLYGON((0 -10, 120 -10, 240 -10, 0 -10))');  
DECLARE @h geography = geography::Parse('POLYGON((0 10, 120 10, 240 10, 0 10))');  
IF (@g.EnvelopeAngle() >= 90)  
BEGIN  
SELECT @g.MinDbCompatibilityLevel();  
END     
IF (@h.EnvelopeAngle() < 90)  
BEGIN  
SELECT @h.MinDbCompatibilityLevel();  
END  
  
```  
  
 第一個 SELECT 陳述式傳回 110，第二個 SELECT 陳述式則傳回 100。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [SQL Server Database Engine 回溯相容性](../../database-engine/sql-server-database-engine-backward-compatibility.md)  
  
  
