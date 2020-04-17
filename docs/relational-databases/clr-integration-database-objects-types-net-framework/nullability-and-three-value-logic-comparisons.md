---
title: 空和三值邏輯比較 |微軟文件
description: 本文介紹了 SQL Server 數據類型與 System.Data.SqlTypes 中的類型有何不同,這些類型具有相似的語義和精度。
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
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488437"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>Null 屬性和三值邏輯比較
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  如果您熟悉資料類型,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您將在**System.Data.SqlType**命名空間中找到類似的語義和[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]精度。 不過，其中仍有一些差異，而且本主題將涵蓋最重要的差異。  
  
## <a name="null-values"></a>NULL 值  
 原生 Common Language Runtime (CLR) 資料類型與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型之間的主要差異是，前者不允許使用 NULL 值，而後者會提供完整的 NULL 語意。  
  
 比較會受到 NULL 值的影響。 比較 x 和 y 這兩個值時，如果 x 或 y 為 NULL，則某些邏輯比較就會評估為 UNKNOWN 值，而非 true 或 false。  
  
## <a name="sqlboolean-data-type"></a>SqlBoolean 資料類型  
 **系統.Data.SqlType**命名空間引入了**SqlBoolean**類型來表示此 3 值邏輯。 任何**SqlType**之間的比較都傳回**SqlBoolean**值類型。 未知值由**SqlBoolean**類型的空值表示。 提供屬性**IsTrue** **、IsFalse**和**IsNull**用於檢查**SqlBoolean**類型的值。  
  
## <a name="operations-functions-and-null-values"></a>作業、函數和 NULL 值  
 所有算術運算符(+、-、/、%)\*位運算符(*、& 和 *),如果**SqlTypes**的任何操作數或參數為 NULL,則大多數函數將返回 NULL。 **IsNull**屬性始終返回真值或假值。  
  
## <a name="precision"></a>Precision  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 中的十進位資料類型與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的數值和十進位資料類型具有不同的最大值。 此外，[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 十進位資料類型會採用最大有效位數。 但是,在的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]CLR 中 **,SqlDecimal**提供了與[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的十進位數據類型相同的最大精度和比例,以及相同的語義。  
  
## <a name="overflow-detection"></a>溢位偵測  
 在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 中，兩個非常龐大的數字相加可能不會擲回例外狀況。 不過，如果沒有使用任何檢查運算子，傳回的結果可能會「循環使用」成為負整數。 在**System.Data.SqlTypes 中**,對所有溢出和下溢錯誤以及除以零的錯誤都引發異常。  
  
## <a name="see-also"></a>另請參閱  
 [.NET Framework 的 SQL Server 資料類型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
