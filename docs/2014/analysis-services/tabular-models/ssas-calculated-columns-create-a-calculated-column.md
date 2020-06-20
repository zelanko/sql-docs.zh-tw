---
title: 建立計算結果欄（SSAS 表格式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.as.daxref.CreataCalculatedColumn.f1
ms.assetid: 59440510-2d76-41dc-9b55-edc15259f9da
author: minewiskan
ms.author: owend
ms.openlocfilehash: a455cdda48fc74027dd22c4915d8384a8b4dae54
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938619"
---
# <a name="create-a-calculated-column-ssas-tabular"></a>建立導出資料行 (SSAS 表格式)
  導出資料行可讓您將新資料加入至模型。 您可以建立 DAX 公式來定義資料行的資料列層級值，而不是將值貼入或匯入資料行。 當您建立有效的公式，然後按一下 ENTER 時，即會計算並填入導出資料行之每個資料列中的值。 然後導出資料行就可以像是其他任何資料行，加入至報表應用程式或分析應用程式。 此主題描述如何在模型設計師中使用 DAX 公式列，來建立新的導出資料行。  
  
#### <a name="to-create-a-new-calculated-column"></a>建立新的導出資料行  
  
1.  在模型設計師的 [資料檢視] 中，選取您要加入導出資料行的資料表，然後按一下 **[資料行]** 功能表，再按一下 **[加入資料行]**。  
  
     **[加入資料行]** 將反白顯示於最右側空白資料行，而且游標會移到公式列。  
  
     若要在兩個現有的資料行之間建立新資料行，請以滑鼠右鍵按一下現有的資料行，然後按一下 [插入資料行]****。  
  
2.  在公式列中，執行下列其中一項：  
  
    -   輸入等號，後面接著公式。  
  
    -   輸入等號，後面接著 DAX 函數，然後是函數需要的引數和參數。  
  
    -   按一下函數按鈕 (**fx**)，然後在 [插入函數]**** 對話方塊中，選取類別目錄和函數，再按一下 [確定]****。 在公式列中，輸入函數所需的其餘引數和參數。  
  
3.  按下 ENTER 鍵接受公式。  
  
     整個資料行都會填入公式，而且會針對每個資料列計算值。  
  
> [!TIP]  
>  您可以透過巢狀函數，在現有的公式中間使用 DAX 公式自動完成。 插入點前方的文字用於顯示下拉式清單中的值，而在插入點之後的所有文字則維持不變。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SSAS 表格式&#41;的計算結果欄](ssas-calculated-columns.md)   
 [量值 &#40;SSAS 表格式&#41;](measures-ssas-tabular.md)  
  
  
