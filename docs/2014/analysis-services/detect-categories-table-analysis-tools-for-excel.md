---
title: 偵測類別目錄 （適用於 Excel 的資料表分析工具） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- clustering [data mining]
- mining model, decision tree
- category detection
ms.assetid: 3c7e9ebb-d0c9-498e-a9ba-cc13eaa43520
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 572c331cb5f9a88ee78cb26544772b126405c02c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62732222"
---
# <a name="detect-categories-table-analysis-tools-for-excel"></a>偵測類別目錄 (適用於 Excel 的資料表分析工具)
  ![功能區中的偵測類別目錄按鈕](media/tat-detectcat.gif "功能區中的 [偵測類別目錄] 按鈕")  
  
 **偵測類別目錄**工具會自動尋找具有類似特性的資料表中資料列。  
  
 當工具完成時，它會建立報表，其中列出找到的類別目錄及其區別特性。 根據預設，它會將新的資料行加入每一個資料列都包含建議類別目錄的資料表。 然後，您就可以檢閱類別目錄並將它們重新命名。  
  
## <a name="using-the-detect-categories-tool"></a>使用偵測類別目錄工具  
  
1.  開啟 Excel 資料表。  
  
2.  按一下 **偵測類別目錄**。  
  
3.  指定要用於分析的資料行。 您可以取消選取有相異值的資料行，例如個人名稱或記錄識別碼，因為這些資料行對分析可能沒有協助。  
  
4.  選擇性地指定要建立的最大類別目錄數目。 根據預設，此工具找到多少類別目錄，就會自動建立一樣多的類別目錄。  
  
5.  按一下 **[執行]**。  
  
6.  工具會建立名為「類別目錄報表」的新工作表，其中包含類別目錄清單及其特性。  
  
 如需如何指定工具選項的詳細資訊，請參閱[偵測類別目錄對話方塊 （適用於 Excel 的資料表分析工具）](detect-categories-table-analysis-tools-for-excel.md)。  
  
## <a name="understanding-the-categories-report"></a>了解類別目錄報表  
 **類別目錄報表**包含兩個資料表，**類別目錄清單**並**類別目錄特性**，以及**類別目錄設定檔**圖表。  
  
### <a name="category-list"></a>類別目錄清單  
 第一個資料表列出找到的類別目錄。 **資料列計數**資料行會指出多少個資料列指派給每個類別目錄。  
  
 模型會為每個類別目錄建立暫時名稱，但您可以視需要重新命名類別目錄。 例如，在下列範例中，第一個類別目錄已重新命名**Low Income**，因為這是叢集的首要屬性。  
  
 ![偵測類別目錄工具所建立的報表](media/dm13-tat-detectcat-report1.gif "偵測類別目錄工具所建立的報表")  
  
 一旦您輸入新標籤，變更就會傳播至所有其他圖表以及加入來源資料工作表中的類別目錄清單。  
  
### <a name="category-characteristics"></a>類別目錄特性  
 第二個資料表中，**類別目錄特性**，顯示每個類別目錄的結構的詳細資料。 按一下 **篩選條件**頂端的按鈕**分類**即可看見焦點位於一個或少數類別的資料行。  
  
 ![偵測類別目錄工具所建立的報表](media/dm13-tat-detectcat-report2.gif "偵測類別目錄工具所建立的報表")  
  
 資料行的陰影**相對的重要性**，指出如何很重要的屬性和值的組合做為區別因數。 垂直線越長，此屬性代表此類別目錄的可能性就越高。  
  
### <a name="categories-profile-chart"></a>類別目錄設定檔圖表  
 中的最後一個圖表**類別目錄報表**工作表**類別目錄設定檔**，是一份互動式**樞紐分析圖**可用來重新排列和隱藏欄位、 篩選值以及自訂圖表的外觀。  
  
 Excel 2013 現在提供**圖表樣式**並**圖表項目**控制項在設計介面，讓您輕鬆地改善圖表設計。  
  
 ![偵測類別目錄工具所建立的報表](media/dm13-tat-detectcat-report3.gif "偵測類別目錄工具所建立的報表")  
  
## <a name="requirements"></a>需求  
 **偵測類別目錄**工具數量或類型的資料沒有任何需求。  
  
> [!NOTE]  
>  當您使用**偵測類別目錄**工具，它會建立新的資料行，類別目錄資料表中的原始資料。 如果您將這個資料行保留在資料表中，接著執行後續的資料採礦作業，這個資料行的存在可能會影響結果。 為了確保不影響其他作業，在使用其他資料採礦工具之前，您應該複製不含類別目錄資料行的資料表。  
  
## <a name="related-tools"></a>相關工具  
 當**偵測類別目錄**工具在分析資料時，它可以建立資料採礦結構和資料採礦模型使用[!INCLUDE[msCoName](../includes/msconame-md.md)]群集演算法。  
  
 您已使用，以建立資料採礦模型之後**分析關鍵影響因數**工具，您可以使用適用於 Excel 的資料採礦用戶端瀏覽此模型，並探索更多詳細資料中的關聯性。 適用於 Excel 的資料採礦用戶端是獨立的增益集，提供更多進階資料採礦功能。 如需資訊，請參閱[Excel 中的 瀏覽模型&#40;SQL Server 資料採礦增益集&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)。  
  
 如需使用資料模型化適用於 Excel 的資料採礦用戶端功能的詳細資訊，請參閱[建立資料採礦模型](creating-a-data-mining-model.md)。  
  
 如需有關所使用的演算法**偵測類別目錄**工具，請參閱中的 < Microsoft 群集演算法 > 主題[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]線上叢書 》。  
  
## <a name="see-also"></a>另請參閱  
 [適用於 Excel 的資料表分析工具](table-analysis-tools-for-excel.md)  
  
  
