---
title: 重定標籤 （SQL Server 資料採礦增益集） |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 5471720cbd3084c661dec93d9c7f4f680e066b86
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66070396"
---
# <a name="relabel-sql-server-data-mining-add-ins"></a>重定標籤 (SQL Server 資料採礦增益集)
  ![重定標籤工具的 office 13 圖示](media/dm13-relabel.gif "重定標籤工具的 Office 13 圖示")  
  
 適用於 Excel 的資料採礦用戶端可協助您建立資料的新標籤，讓分析結果更容易理解。  
  
 重定標籤的原因包括：  
  
-   資料包含的結果經過編碼，例如 1 代表男性，2 代表女性。  
  
-   您要建立數值的值區，並且想要為範圍指定描述性名稱。  
  
-   您想要簡化完整名稱。  
  
## <a name="using-the-relabel-wizard"></a>使用重定標籤精靈  
  
1.  在 **資料採礦**功能區中，按一下**清除**，然後選取**重定標籤**。  
  
2.  選取含有您要修正之資料的資料表或資料範圍。  
  
3.  在 **重定標籤**頁面的精靈中，選取單一資料行，從下拉式清單中，選擇資料行，或按一下中的資料行**資料範例**窗格。  
  
     **資料範例**窗格只會顯示大約 50 個資料列，但它們已經過取樣可確保您看到分散良好的值。  
  
     按一下資料行標頭**計數**來排序每個值的計數。  
  
     您也可以依排序**原始標籤**，這會很方便，如果您想要重新第一次標示所有最高或最低值。  
  
4.  在 **重定標籤**資料頁面上，在精靈的檢閱中的值**原始標籤**資料行，並決定您要群組或編輯它們的方式。  
  
5.  底下的資料列中輸入新的值**新的標籤**。 您可以從現有值的清單中選取某個值。 輸入新的值時，它們會立即成為可供重複使用。  
  
6.  當您輸入足夠的資料列時，按一下**下一步**，然後在**選取目的地**頁面上，選擇您要在其中儲存重定標籤之的資料。  
  
    -   **以新的資料行加入目前的工作表**  
  
         按一下即可將新資料行加入包含新值的資料表。  
  
    -   **將包含變更的工作表資料複製到新的工作表**  
  
         按一下即可建立包含更新資料的新工作表。  
  
    -   **就地變更資料**  
  
         按一下即可將原始資料取代成新值。  
  
## <a name="see-also"></a>另請參閱  
 [瀏覽和清除資料](exploring-and-cleaning-data.md)  
  
  
