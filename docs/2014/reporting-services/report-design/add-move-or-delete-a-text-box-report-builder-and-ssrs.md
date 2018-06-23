---
title: 新增、移動或刪除文字方塊 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f042cf81-d933-4ac7-9287-c074a46bde98
caps.latest.revision: 5
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 2023c9a066d2a9f0e9507fe0c06dcab4fbcc66a9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137234"
---
# <a name="add-move-or-delete-a-text-box-report-builder-and-ssrs"></a>加入、移動或刪除文字方塊 (報表產生器及 SSRS)
  文字方塊是報表中最常使用的報表項目。 您可以將文字方塊加入至報表主體，以便顯示標題、參數選擇、內建欄位和日期等資訊。  
  
 資料表或矩陣中的每個資料格實際上都是文字方塊。 幾乎所有顯示在報表中的報表資料 (包含資料表和矩陣) 都是報表處理器評估報表中每一個文字方塊內容的結果。 因此，您可以利用在資料區外部格式化其他文字方塊的相同方式，格式化資料格。  
  
 若要將文字方塊加入至清單資料區，您必須先加入此文字方塊，然後將它拖曳到清單中。  
  
> [!NOTE]  
>  當您按一下文字方塊時，就可以立即編輯文字方塊中的文字。 若要選取文字方塊本身，而非其中的文字，請按下 ESC。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-text-box"></a>若要加入文字方塊  
  
1.  在 [設計] 檢視的 **[插入]** 索引標籤上，按一下 **[文字方塊]**。  
  
2.  在設計介面中，按一下然後將方塊拖曳至所需的文字方塊大小。 另外，您也可以按一下設計介面來建立預設大小的文字方塊。  
  
### <a name="to-add-a-text-box-in-a-list"></a>若要在清單中加入文字方塊  
  
1.  在 [報表設計] 檢視的 **[插入]** 索引標籤上，按一下 **[清單]**。  
  
2.  在設計介面中，按一下然後將方塊拖曳至所需的清單大小。 另外，您也可以按一下設計介面來建立預設大小的清單。  
  
3.  在 **[插入]** 索引標籤上，按一下 **[文字方塊]**。  
  
4.  在設計介面中，於步驟 1 加入的清單內部，按一下然後將方塊拖曳至所需的文字方塊大小。 或者，按一下在清單內部的設計介面，即可建立預設大小的文字方塊。  
  
5.  若要確認文字方塊以巢狀結構的方式正確置於清單內，請選取此文字方塊。  
  
    > [!NOTE]  
    >  如果您在文字方塊中按一下並且處於編輯模式，請按下 ESC 來選取文字方塊。  
  
6.  在 [屬性] 窗格內，確認 **[Parent]** 屬性是自動加入至清單資料區的矩形。  
  
    > [!NOTE]  
    >  如果看不到 [屬性] 窗格，請核取 [檢視] 索引標籤上的 [屬性]。  
  
### <a name="to-move-a-text-box"></a>若要移動文字方塊  
  
1.  在 [報表設計] 檢視中，按一下文字方塊內的任何空白處，即可選取該文字方塊。  
  
    > [!NOTE]  
    >  如果您在文字方塊中按一下並且處於編輯模式，請按下 ESC 來選取文字方塊。  
  
2.  按一下文字方塊控點，並將文字方塊拖曳到新的位置。 另外，您也可以使用方向鍵，水平或垂直移動選取的文字方塊。 若要在設計介面上以較小的增量來移動文字方塊，請按住 CTRL 鍵的同時再按方向鍵。  
  
### <a name="to-delete-a-text-box"></a>若要刪除文字方塊  
  
1.  在 [報表設計] 檢視中，以滑鼠右鍵按一下文字方塊內的任何空白處來選取它，然後按一下 [刪除]。 或者，按一下文字方塊內的任何空白處，然後按 DELETE 鍵。  
  
    > [!NOTE]  
    >  如果您在文字方塊中按一下並且處於編輯模式，請按下 ESC 來選取文字方塊。  
  
## <a name="see-also"></a>另請參閱  
 [文字方塊&#40;報表產生器和 SSRS&#41;](text-boxes-report-builder-and-ssrs.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [鍵盤快速鍵&#40;報表產生器&#41;](../report-builder/keyboard-shortcuts-report-builder.md)  
  
  