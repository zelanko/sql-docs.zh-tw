---
title: 雜湊索引 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f4bdc9c1-7922-4fac-8183-d11ec58fec4e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 420cf534b57dc6b6592b4dd55cf5ec2addd04b2a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84932859"
---
# <a name="hash-indexes"></a>雜湊索引
  索引做為記憶體最佳化資料表的進入點。 讀取資料表的資料列需要索引，以找出記憶體中的資料。  
  
 雜湊索引包含以陣列方式組織的貯體集合。 雜湊函數會將索引鍵對應到雜湊索引中的對應貯體。 下圖顯示三個索引鍵對應到雜湊索引中的三個不同貯體。 為了提供說明，雜湊函數名稱為 f(x)。  
  
 ![對應到不同貯體的索引鍵。](../../2014/database-engine/media/hekaton-tables-2.gif "對應到不同貯體的索引鍵。")  
  
 用於雜湊索引的雜湊函數具有下列特性：  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 有一個雜湊函數可用於所有雜湊索引。  
  
-   該雜湊函數具決定性。 相同索引鍵永遠對應到雜湊索引中的相同貯體。  
  
-   多個索引鍵可能對應至相同的雜湊值區。  
  
-   平衡雜湊函數，表示索引鍵值在雜湊值區上的分配通常會遵循波氏分配。  
  
     波氏分配不是平均分配。 索引鍵值不會平均分佈在雜湊值區中。 例如，在*n*個雜湊值區的*n*個相異索引鍵的波氏分佈，會產生大約一個第三個空值區，其中第一個包含一個索引鍵的值區，另一個則包含兩個索引鍵。 少數貯體會包含兩個以上的索引鍵。  
  
 如果兩個索引鍵對應到相同雜湊值區，就會發生雜湊衝突。 大量的雜湊衝突可能會對讀取作業產生效能影響。  
  
 記憶體中雜湊索引包含記憶體指標陣列。 每個貯體對應到這個陣列中的位移。 陣列中的每個貯體指向該雜湊值區的第一個資料列。 貯體中的每個資料列指向下一個資料列，因而造成每個雜湊值區的資料列鏈結，如下圖所示。  
  
 ![記憶體中的雜湊索引結構。](../../2014/database-engine/media/hekaton-tables-3.gif "記憶體中的雜湊索引結構。")  
  
 此圖中有三個貯體包含資料列。 最上方第二個貯體包含三個紅色資料列。 第四個貯體包含單一藍色資料列。 最下方的貯體包含兩個綠色資料列。 這些可能是相同資料列的不同版本。  
  
 如需記憶體優化資料表之索引的詳細資訊，請參閱[在記憶體優化資料表上使用索引的指導方針](../relational-databases/in-memory-oltp/memory-optimized-tables.md)。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體最佳化資料表上的索引](../../2014/database-engine/indexes-on-memory-optimized-tables.md)  
  
  
