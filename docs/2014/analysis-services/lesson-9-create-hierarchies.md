---
title: 第 10 課： 建立階層 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
caps.latest.revision: 16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3b8b1b0b3c38374061361df9980c74cfb6e5cbf9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37247818"
---
# <a name="lesson-10-create-hierarchies"></a>第 10 課：建立階層
  在這一課，您將建立階層。 階層是以層級排列的資料行群組；例如，[地理位置] 階層可能有 [國家/地區]、[州省]、[縣市]、[縣 (市)] 的子層級。 在報表用戶端應用程式欄位清單中，階層可以與其他資料行分開顯示，讓用戶端使用者更易於導覽及包含在報表中。 如需詳細資訊，請參閱[ &#40;SSAS 表格式&#41;](tabular-models/hierarchies-ssas-tabular.md)。  
  
 若要建立階層，您將使用 [圖表檢視] 中的模型設計師。 不支援在模型設計師的 [資料檢視] 中建立及管理階層。  
  
 完成本課程的估計時間： **20 分鐘**  
  
## <a name="prerequisites"></a>先決條件  
 本主題是表格式模型教學課程的一部分，必須依序完成。 在執行本課程的工作之前，您應已完成上一課：[第 9 課：建立檢視方塊](lesson-8-create-perspectives.md)。  
  
## <a name="create-hierarchies"></a>建立階層  
  
#### <a name="to-create-a-category-hierarchy-in-the-product-table"></a>在產品資料表中建立類別目錄階層  
  
1.  在模型設計師中，按一下`Model`功能表，然後指向**模型檢視**，然後按一下**圖表檢視**。  
  
    > [!TIP]  
    >  使用模型設計師右上方的 [迷你地圖] 控制項，即可變更您可以在 [圖表檢視] 中檢視物件的方式。 如果您將物件重新定位在 [圖表檢視] 中，該檢視會在您儲存專案時保留。  
  
2.  在模型設計師中，以滑鼠右鍵按一下`Product`資料表，然後按一下**建立階層**。 新的階層會出現在資料表視窗的底部。  
  
3.  在階層名稱中，重新命名該階層輸入`Category`，然後按 ENTER 鍵。  
  
4.  在`Product`資料表中，按一下**Product Category Name**資料行，然後將它拖曳至`Category`階層，以及然後的頂部放開`Category`名稱。  
  
5.  在`Category`階層中，以滑鼠右鍵按一下**Product Category Name**資料行，然後按一下**重新命名**，然後輸入`Category`。  
  
    > [!NOTE]  
    >  重新命名階層中的資料行並不會重新命名資料表中的該資料行。 階層中的資料行只是資料表中資料行的表示。  
  
6.  在`Product`資料表中，以滑鼠右鍵按一下**Product Subcategory Name**資料行，然後在操作功能表，指向**新增至階層**，然後按一下  `Category`。  
  
7.  重新命名**Product Subcategory Name**至`Subcategory`。  
  
8.  使用按一下並拖曳，或使用**新增至階層**命令的內容功能表中，新增**模型名稱**並**產品名稱**（依順序） 的資料行，然後將這些下方**Product Subcategory Name**資料行。 重新命名這些資料行`Model`和`Product`分別。  
  
#### <a name="to-create-hierarchies-in-the-date-table"></a>在日期資料表中建立階層  
  
1.  在模型設計師中，以滑鼠右鍵按一下 [日期] 資料表，然後按一下 [建立階層]。  
  
2.  將階層重新命名為 **Calendar**。  
  
3.  依序加入下列資料行，然後將它們重新命名：  
  
    |「資料行」|重新命名為：|  
    |------------|----------------|  
    |Calendar Year|Year|  
    |Calendar Semester|半年度|  
    |Calendar Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
4.  在 [日期] 資料表中重複上述步驟，建立 [Fiscal] 階層，包括下列資料行：  
  
    |「資料行」|重新命名為：|  
    |------------|----------------|  
    |Fiscal Year|Year|  
    |Fiscal Semester|半年度|  
    |Fiscal Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
5.  最後，在 [日期] 資料表中重複上述步驟，建立 [Production Calendar] 階層，包括下列資料行：  
  
    |「資料行」|重新命名為：|  
    |------------|----------------|  
    |Calendar Year|Year|  
    |Week Number Of Year|週|  
    |週中的日|Day|  
  
## <a name="next-steps"></a>後續步驟  
 若要繼續進行本教學課程，請前往下一課：[第 11 課：建立資料分割](lesson-10-create-partitions.md)。  
  
  
