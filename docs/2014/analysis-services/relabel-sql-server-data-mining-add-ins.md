---
title: 重新標記（SQL Server 資料採礦增益集） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data preparation
- relabel
- data cleaning
ms.assetid: af041b39-fdd1-4cb5-a5ef-2f3ddab84614
author: minewiskan
ms.author: owend
ms.openlocfilehash: 7473f9c4dd9080fc03d3b1dea106f8b10c9c2916
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84539435"
---
# <a name="relabel-sql-server-data-mining-add-ins"></a>重定標籤 (SQL Server 資料採礦增益集)
  ![[重定標籤] 工具的 Office 13 圖示](media/dm13-relabel.gif "[重定標籤] 工具的 Office 13 圖示")

 適用於 Excel 的資料採礦用戶端可協助您建立資料的新標籤，讓分析結果更容易理解。

 重定標籤的原因包括：

-   資料包含的結果經過編碼，例如 1 代表男性，2 代表女性。

-   您要建立數值的值區，並且想要為範圍指定描述性名稱。

-   您想要簡化完整名稱。

## <a name="using-the-relabel-wizard"></a>使用重定標籤精靈

1.  在 [**資料採礦**] 功能區中，按一下 [**清除**]，然後選取 [**重新標籤**]。

2.  選取含有您要修正之資料的資料表或資料範圍。

3.  在嚮導的 [**重新標籤**] 頁面中，從下拉式清單中選擇資料行，或按一下 [**資料範例**] 窗格中的資料行，以選取單一資料行。

     [**資料範例**] 窗格只會顯示大約50個數據列，但會進行取樣，以確保您看到值的良好散佈。

     按一下 [**計數**] 的資料行標題，依每個值的計數排序。

     您也可以依**原始卷**標排序，如果您想要先重新標示所有最高或最低值，這會很方便。

4.  在嚮導的 [**重新標籤**資料] 頁面中，檢查 [**原始標籤**] 欄中的值，並決定您要將它們分組或編輯的方式。

5.  在 [**新標籤**] 底下的資料列中輸入新的值。 您可以從現有值的清單中選取某個值。 輸入新的值時，它們會立即成為可供重複使用。

6.  當您輸入足夠的資料列時，請按 **[下一步]**，然後在 [**選取目的地**] 頁面上，選擇您要儲存重新標示資料的位置。

    -   **加入目前工作表中成為新資料行**

         按一下即可將新資料行加入包含新值的資料表。

    -   **將包含變更的工作表資料複製到新工作表**

         按一下即可建立包含更新資料的新工作表。

    -   **就地變更資料**

         按一下即可將原始資料取代成新值。

## <a name="see-also"></a>另請參閱
 [瀏覽和清除資料](exploring-and-cleaning-data.md)


