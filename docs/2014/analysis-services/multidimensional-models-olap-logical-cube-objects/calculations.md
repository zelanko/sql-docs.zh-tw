---
title: 計算 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- calculations [Analysis Services]
- OLAP objects [Analysis Services], calculations
- MDX [Analysis Services], calculations
- calculations [Analysis Services], about calculations
- cubes [Analysis Services], calculations
ms.assetid: 6be84916-fd05-4efc-ab98-6adbbad80154
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8ef953f375269917a7cab7d00a15def6acfb375e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37222188"
---
# <a name="calculations"></a>[新增命名集]
  計算是多維度運算式 (MDX) 運算式或指令碼，用來定義 cube 中的導出的成員、 命名的集或範圍的指派[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 計算可讓您加入的物件不是由 Cube 之資料所定義，而是由參考 Cube 之其他部分、其他 Cube 甚至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫外部之資訊的運算式所定義。 計算可讓您擴充 Cube 的功能，以在商業智慧應用程式中加入彈性和強大功能。 如需有關指令碼計算的詳細資訊，請參閱[Introduction to Microsoft SQL Server 2005 中 MDX 指令碼](http://go.microsoft.com/fwlink/?LinkId=81892)。 如需 MDX 查詢和計算相關效能問題的詳細資訊，請參閱[SQL Server 2005 Analysis Services 效能指南](http://go.microsoft.com/fwlink/?LinkId=81621)。  
  
## <a name="calculated-members"></a>導出成員  
 導出成員是使用您在定義導出成員時指定的多維度運算式 (MDX) 運算式，以在執行階段計算出其值的成員。 與其他任何成員一樣，商業智慧應用程式也可以使用導出成員。 因為在 Cube 中只會儲存定義，所以導出成員並不會增加 Cube 的大小；需要回答查詢時才會在記憶體中計算出值。  
  
 可以針對任何維度定義導出成員，包括量值維度。 在量值維度上建立的導出成員，稱為導出量值。  
  
 雖然導出成員通常是根據 Cube 中的現有資料，但是您也可以將資料與算術運算子、數字和函數組合來建立複雜的運算式。 您也可使用 MDX 函數 (如 LookupCube) 來存取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中其他 Cube 內的資料； [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包含標準化的 Visual Studio 函數程式庫，而且您可使用預存程序從目前 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫以外的來源中擷取資料。 如需有關預存程序的詳細資訊，請參閱 <<c0> [ 定義的預存程序](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)。  
  
 例如，假設一運輸公司的管理者想要根據每一容量單位的利潤，來決定運送哪一種貨物類型的利潤較高。 他們使用包含貨物、船隊與時間維度，以及 Price_to_Ship、Cost_to_Ship、及 Volume_in_Cubic_Meters 量值的運貨 Cube；但是，該 Cube 沒有包含獲利率的量值。 您可以在下列運算式中合併現有的量值，以在 Cube 中建立一個導出成員作為量值 (名為 Profit_per_Cubic_Meter)：  
  
```  
([Measures].[Price_to_Ship] - [Measures].[Cost_to_Ship]) /  
[Measures].[Volume_in_Cubic_Meters]  
```  
  
 建立導出成員後，Profit_per_Cubic_Meter 會在下次瀏覽運貨 Cube 時，與其他量值一起出現。  
  
 若要建立導出的成員，請使用**計算**的標籤，Cube 設計師中。 如需詳細資訊，請參閱[建立導出成員](../multidimensional-models/create-calculated-members.md)  
  
## <a name="named-sets"></a>命名集  
 命名集是會傳回集合的 CREATE SET MDX 陳述式運算式； MDX 運算式會儲存為 cube 中定義的一部分[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 建立命名集，以供在多維度運算式 (MDX) 查詢中重複使用。 命名集可讓商務使用者簡化查詢，以及針對複雜且常用的集合運算式來使用集合名稱 (而非集合運算式)。 **相關的主題：** [建立命名集](../multidimensional-models/create-named-sets.md)  
  
## <a name="script-commands"></a>指令碼命令  
 指令碼命令是 MDX 指令碼，包含在 Cube 的定義中。 指令碼命令幾乎可讓您在 Cube 上執行 MDX 所支援的任何動作 (例如，設定計算的範圍使其只適用於 Cube 的一部分)。 在  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，MDX 指令碼可以套用至整個 cube 或特定的 cube，在特定時間點執行作業的指令碼區段。 預設指令碼命令 (CALCULATE 陳述式) 會使用根據預設範圍的彙總資料來填入 Cube 中的資料格。  
  
 預設範圍就是整個 Cube，但您可以定義更小的範圍，即所謂的 Subcube，然後將 MDX 指令碼只套用至該特定 Cube 空間。 SCOPE 陳述式會在計算指令碼中定義所有後續 MDX 運算式和陳述式的範圍，直到範圍終止或重新定義為止。 然後使用 THIS 陳述式，將 MDX 運算式至目前範圍。 您可以使用 BACK_COLOR 陳述式，指定目前範圍內資料格的背景資料格顏色，以協助您進行偵錯。  
  
 例如，您可以使用指令碼命令，依據之前時間週期的銷售的加權值，將銷售配額配置給跨越時間和銷售地區的員工。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的計算](../multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
