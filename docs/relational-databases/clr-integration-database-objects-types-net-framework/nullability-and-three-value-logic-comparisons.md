---
title: Null 屬性和三值邏輯比較 |Microsoft Docs
description: 本文涵蓋 SQL Server 資料類型與 .NET Framework 中 SqlTypes 的類型有何不同，其具有類似的語法和精確度。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: 3f016abf2113afef3e02f01fd9842b91b742d50a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488437"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>Null 屬性和三值邏輯比較
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  如果您熟悉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型，則會在的[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] **SqlTypes**命名空間中找到類似的語義和有效位數。 不過，其中仍有一些差異，而且本主題將涵蓋最重要的差異。  
  
## <a name="null-values"></a>NULL 值  
 原生 Common Language Runtime (CLR) 資料類型與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型之間的主要差異是，前者不允許使用 NULL 值，而後者會提供完整的 NULL 語意。  
  
 比較會受到 NULL 值的影響。 比較 x 和 y 這兩個值時，如果 x 或 y 為 NULL，則某些邏輯比較就會評估為 UNKNOWN 值，而非 true 或 false。  
  
## <a name="sqlboolean-data-type"></a>SqlBoolean 資料類型  
 **SqlTypes**命名空間引進了**SqlBoolean**類型來代表這個3值邏輯。 任何**SqlTypes**的比較都會傳回**SqlBoolean**數值型別。 未知的值是以**SqlBoolean**類型的 null 值表示。 會提供屬性**IsTrue**、 **IsFalse**和**IsNull** ，以檢查**SqlBoolean**類型的值。  
  
## <a name="operations-functions-and-null-values"></a>作業、函數和 NULL 值  
 如果 SqlTypes 的任何運算元或引數\*為 null，則所有算術運算子（+、-、、/、%）、位運算子（~、& 和 |）和大部分**SqlTypes**函數都會傳回 null。 **IsNull**屬性一律會傳回 true 或 false 值。  
  
## <a name="precision"></a>Precision  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 中的十進位資料類型與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的數值和十進位資料類型具有不同的最大值。 此外，[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 十進位資料類型會採用最大有效位數。 不過，在的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]CLR 中， **SqlDecimal**會提供相同的最大有效位數和小數位數，以及與中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 decimal 資料類型相同的語義。  
  
## <a name="overflow-detection"></a>溢位偵測  
 在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 中，兩個非常龐大的數字相加可能不會擲回例外狀況。 不過，如果沒有使用任何檢查運算子，傳回的結果可能會「循環使用」成為負整數。 在**SqlTypes**中，會針對所有溢位和下溢錯誤和零除的錯誤擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [.NET Framework 的 SQL Server 資料類型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
