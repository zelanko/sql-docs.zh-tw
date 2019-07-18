---
title: Null 屬性和三值邏輯比較 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- precision [CLR integration]
- overflow detections [CLR integration]
- null values [CLR integration]
- three-value logic comparisons [CLR integration]
- data types [CLR integration]
- SqlBoolean data type
ms.assetid: 13da4c7f-1010-4b2d-a63c-c69b6bfd96f1
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4f1b4823db4ae961024ac2a786c948d8349f31be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62919629"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>Null 屬性和三值邏輯比較
  如果您熟悉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型，就會在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 的 `System.Data.SqlTypes` 命名空間中找到類似的語意和有效位數。 不過，其中仍有一些差異，而且本主題將涵蓋最重要的差異。  
  
## <a name="null-values"></a>NULL 值  
 原生 Common Language Runtime (CLR) 資料類型與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型之間的主要差異是，前者不允許使用 NULL 值，而後者會提供完整的 NULL 語意。  
  
 比較會受到 NULL 值的影響。 比較 x 和 y 這兩個值時，如果 x 或 y 為 NULL，則某些邏輯比較就會評估為 UNKNOWN 值，而非 true 或 false。  
  
## <a name="sqlboolean-data-type"></a>SqlBoolean 資料類型  
 `System.Data.SqlTypes` 命名空間導入了 `SqlBoolean` 類型來代表這個 3 值邏輯。 任何 `SqlTypes` 之間的比較都會傳回 `SqlBoolean` 值類型。 UNKNOWN 值是由 `SqlBoolean` 類型的 Null 值所代表。 系統提供了 `IsTrue`、`IsFalse` 和 `IsNull` 屬性來檢查 `SqlBoolean` 類型的值。  
  
## <a name="operations-functions-and-null-values"></a>作業、函數和 NULL 值  
 所有算術運算子 (+、-， \*，/、 %)，位元運算子 (~、 &、 和 |)，以及大部分函數都會傳回 NULL，如果任何運算元或引數`SqlTypes`都是 NULL。 `IsNull` 屬性一律會傳回 true 或 false 值。  
  
## <a name="precision"></a>有效位數  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 中的十進位資料類型與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的數值和十進位資料類型具有不同的最大值。 此外，[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 十進位資料類型會採用最大有效位數。 不過，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 CLR 中，`SqlDecimal` 會提供相同的最大有效位數和小數位數，以及與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中十進位資料類型相同的語意。  
  
## <a name="overflow-detection"></a>溢位偵測  
 在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 中，兩個非常龐大的數字相加可能不會擲回例外狀況。 不過，如果沒有使用任何檢查運算子，傳回的結果可能會「循環使用」成為負整數。 在 `System.Data.SqlTypes` 中，系統會針對所有溢位和反向溢位錯誤，以及除以零的錯誤擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [.NET Framework 的 SQL Server 資料類型](sql-server-data-types-in-the-net-framework.md)  
  
  
