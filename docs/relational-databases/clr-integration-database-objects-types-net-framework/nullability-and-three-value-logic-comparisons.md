---
title: Null 屬性和三值邏輯比較 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- precision [CLR integration]
- overflow detections [CLR integration]
- null values [CLR integration]
- three-value logic comparisons [CLR integration]
- data types [CLR integration]
- SqlBoolean data type
ms.assetid: 13da4c7f-1010-4b2d-a63c-c69b6bfd96f1
caps.latest.revision: 38
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4a01f167900a0aa64759297f6a3b4b2d2c81cf86
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37356200"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>Null 屬性和三值邏輯比較
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  如果您熟悉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型，您會發現類似的語意和有效位數**System.Data.SqlTypes**中的命名空間[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]。 不過，其中仍有一些差異，而且本主題將涵蓋最重要的差異。  
  
## <a name="null-values"></a>NULL 值  
 原生 Common Language Runtime (CLR) 資料類型與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型之間的主要差異是，前者不允許使用 NULL 值，而後者會提供完整的 NULL 語意。  
  
 比較會受到 NULL 值的影響。 比較 x 和 y 這兩個值時，如果 x 或 y 為 NULL，則某些邏輯比較就會評估為 UNKNOWN 值，而非 true 或 false。  
  
## <a name="sqlboolean-data-type"></a>SqlBoolean 資料類型  
 **System.Data.SqlTypes**命名空間引入**SqlBoolean**來代表這個 3 值邏輯的類型。 任何之間的比較**SqlTypes**會傳回**SqlBoolean**實值型別。 未知的值 null 值來表示**SqlBoolean**型別。 屬性**IsTrue**， **IsFalse**，並**IsNull**若要檢查的值提供**SqlBoolean**型別。  
  
## <a name="operations-functions-and-null-values"></a>作業、函數和 NULL 值  
 所有算術運算子 (+、-， \*，/、 %)，位元運算子 (~、 &、 和 |)，以及大部分函數都會傳回 NULL，如果任何運算元或引數**SqlTypes**都是 NULL。 **IsNull**屬性一律會傳回 true 或 false 的值。  
  
## <a name="precision"></a>有效位數  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 中的十進位資料類型與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的數值和十進位資料類型具有不同的最大值。 此外，[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 十進位資料類型會採用最大有效位數。 中的 CLR [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，不過**SqlDecimal**提供相同的最大有效位數和小數位數和中的十進位資料類型相同的語意[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="overflow-detection"></a>溢位偵測  
 在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 中，兩個非常龐大的數字相加可能不會擲回例外狀況。 不過，如果沒有使用任何檢查運算子，傳回的結果可能會「循環使用」成為負整數。 在  **System.Data.SqlTypes**，所有的溢位和反向溢位錯誤，和除以零錯誤擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [.NET Framework 的 SQL Server 資料類型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
