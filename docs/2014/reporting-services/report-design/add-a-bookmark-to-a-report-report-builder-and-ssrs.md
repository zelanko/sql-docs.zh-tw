---
title: 將書籤新增至報表 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f130562e-5673-40e3-8e01-de7227a21d41
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0031e215c0674f87620e283a7bf903b174a40ae3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106914"
---
# <a name="add-a-bookmark-to-a-report-report-builder-and-ssrs"></a>將書籤加入至報表 (報表產生器及 SSRS)
  當您想要在報表中提供自訂內容資料表或是提供自訂內部導覽連結時，請將書籤或書籤連結加入到報表中。 一般來說，您會在報表中想要引導使用者的位置上加入書籤，例如每一個資料表或圖表的書籤，或是資料表或矩陣內顯示之唯一群組值的標籤。 您可以建立自己的字串當做書籤使用，或是針對群組設定群組運算式的標籤。  
  
 當您建立書籤之後，可以加入使用者只需按一下就可移至每一個書籤的報表項目。 這些項目通常是文字方塊或影像。  
  
 例如，如果您的報表顯示依色彩分組的資料表，您會將根據群組運算式的書籤加入到群組首。 然後您會加入一個具有單一文字方塊的資料表 (此文字方塊位於顯示色彩值的報表開頭)，然後您會在該文字方塊上設定書籤連結。 當您按一下色彩時，報表會跳到頁面，此頁面顯示該色彩的群組首資料列。  
  
 您可以將書籤加入到任何報表項目，並將書籤連結加入到具有 **Action** 屬性的任何項目，例如文字方塊、影像或是圖表中的導出數列。 如需詳細資訊，請參閱[動作屬性對話方塊 &#40;報表產生器及 SSRS&#41;](../action-properties-dialog-box-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-bookmark"></a>加入書籤  
  
1.  在 [報表設計] 檢視中，選取您想要加入書籤的文字方塊、影像、圖表或其他報表項目。 選定項目的屬性會顯示在 [屬性] 窗格中。  
  
2.  在 **[書籤]** 旁邊的文字方塊內，輸入一個字串當做此書籤的標籤。 例如，您可以輸入 **BikePhoto** 做為報表中影像的書籤。 另外，您也可以按一下運算式 (**fx**) 按鈕開啟 [運算式]  對話方塊，以指定評估為標籤的運算式。 如果是群組，您所輸入的運算式應該是群組運算式。  
  
    > [!NOTE]  
    >  書籤可以是任何字串，但它在報表內必須是唯一的。 如果此書籤不是唯一的，書籤的連結會尋找第一個相符的書籤。  
  
### <a name="to-add-a-bookmark-link"></a>加入書籤連結  
  
1.  在 [設計] 檢視中，以滑鼠右鍵按一下要新增連結的文字方塊、影像或圖表，然後按一下 [屬性]  。  
  
2.  在該報表項目的 **[屬性]** 對話方塊中，按一下 **[動作]** 。  
  
3.  選取 **[移至書籤]** 。 此對話方塊中會出現這個選項的其他區段。  
  
4.  在 **[選取書籤]** 方塊中，輸入或選取書籤或評估為書籤的運算式。 使用先前的範例，輸入 **BikePhoto** 來建立報表中影像的連結。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  (選擇性) 文字不會自動格式化為連結的樣式。 如果是文字，則變更文字色彩及效果來指示該文字為連結，將會是很有協助的作法。 例如，在 [功能區] 的 [主資料夾] 索引標籤上設定 **[字型]** 區段，將色彩變更為藍色並加上底線效果。  
  
7.  若要測試連結，請按一下 **[執行]** 預覽報表，然後按一下這個連結設定所在的報表項目。  
  
## <a name="see-also"></a>另請參閱  
 [互動式排序、文件引導模式及連結 &#40;報表產生器及 SSRS&#41;](interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
