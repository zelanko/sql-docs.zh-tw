---
title: 雜湊索引 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f4bdc9c1-7922-4fac-8183-d11ec58fec4e
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: 3da74688d6a2f65b191788ab9ecd2394bcca8597
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037303"
---
# <a name="hash-indexes"></a>雜湊索引
  索引做為記憶體最佳化資料表的進入點。 讀取資料表的資料列需要索引，以找出記憶體中的資料。  
  
 雜湊索引包含以陣列方式組織的貯體集合。 雜湊函數會將索引鍵對應到雜湊索引中的對應貯體。 下圖顯示三個索引鍵對應到雜湊索引中的三個不同貯體。 為了提供說明，雜湊函數名稱為 f(x)。  
  
 ![索引鍵對應到不同貯體。](../../2014/database-engine/media/hekaton-tables-2.gif "索引鍵對應到不同貯體。")  
  
 用於雜湊索引的雜湊函數具有下列特性：  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 有一個雜湊函數可用於所有雜湊索引。  
  
-   該雜湊函數具決定性。 相同索引鍵永遠對應到雜湊索引中的相同貯體。  
  
-   多個索引鍵可能對應至相同的雜湊值區。  
  
-   平衡雜湊函數，表示索引鍵值在雜湊值區上的分配通常會遵循波氏分配。  
  
     波氏分配不是平均分配。 索引鍵值不會平均分佈在雜湊值區中。 例如，波氏分佈的*n*相異索引鍵*n*雜湊值區會導致大約三分之一的空白貯體、 三分之一的貯體包含一個索引鍵和其他第三個包含兩個索引鍵。 少數貯體會包含兩個以上的索引鍵。  
  
 如果兩個索引鍵對應到相同雜湊值區，就會發生雜湊衝突。 大量的雜湊衝突可能會對讀取作業產生效能影響。  
  
 記憶體中雜湊索引包含記憶體指標陣列。 每個貯體對應到這個陣列中的位移。 陣列中的每個貯體指向該雜湊值區的第一個資料列。 貯體中的每個資料列指向下一個資料列，因而造成每個雜湊值區的資料列鏈結，如下圖所示。  
  
 ![In-memory 雜湊索引結構。] (../../2014/database-engine/media/hekaton-tables-3.gif "In-memory 雜湊索引結構。")  
  
 此圖中有三個貯體包含資料列。 最上方第二個貯體包含三個紅色資料列。 第四個貯體包含單一藍色資料列。 最下方的貯體包含兩個綠色資料列。 這些可能是相同資料列的不同版本。  
  
 如需記憶體最佳化資料表的索引的詳細資訊，請參閱[使用記憶體最佳化資料表的索引指導方針](../relational-databases/in-memory-oltp/memory-optimized-tables.md)。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體最佳化資料表上的索引](../../2014/database-engine/indexes-on-memory-optimized-tables.md)  
  
  