---
title: 分析關鍵影響因數 （適用於 Excel 的資料表分析工具） |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Table Analysis tools
- key influencers
- factor analysis
ms.assetid: 54d7b4ce-7b79-407a-985c-aa655ad19280
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 41b30eb0f3f0dc68c5666581a2682470fac7f978
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032018"
---
# <a name="analyze-key-influencers-table-analysis-tools-for-excel"></a>分析關鍵影響因數 (適用於 Excel 的資料表分析工具)
  ![功能區中的 分析關鍵影響因數按鈕](media/tat-aki.gif "功能區中的 分析關鍵影響因數按鈕")  
  
 與**分析關鍵影響因數**工具中，選擇包含目標結果的資料行，而演算法會判斷哪些因數有最強的影響力，結果。  
  
 此工具會建立新的資料表，此資料表會報告與每一個結果有關的因數，並以圖形方式顯示此關聯性的機率。 您可以依據不同的因數和結果來篩選資料表，以瀏覽更深層的結果。  
  
 您也可以選取一對可能的結果，並加以比較。 例如，您可能會比較不同的消費者群組以判斷可能的決策因數。  
  
## <a name="using-the-analyze-key-influencers-tool"></a>使用分析關鍵影響因數工具  
  
1.  開啟 Excel 資料表。  
  
2.  在**資料表工具**上**分析**功能區中，按一下 **分析關鍵影響因數。**  
  
3.  選取要當做分析目標的單一資料行。  
  
4.  （選擇性） 按一下**選擇用於分析的資料行**。 在**進階資料行選取**對話方塊方塊中，選擇最有可能包含相關資料的資料行。 若要提升效能和精確度，請取消選取對於模式分析不重要的資料行，如識別碼或名稱。 按一下**確定**關閉**進階資料行選取** 對話方塊。  
  
5.  按一下 **[執行]**。  
  
     **分析關鍵影響因數**工具進行的分析資料來判斷最佳的設定，並自動設定所有參數。  
  
6.  如果未偵測到任何模式，此精靈便會建立包含問題描述的新工作表。  
  
7.  如果偵測到模式，此精靈會在新的工作表上建立報表來顯示模式。 此報表稱為**的關鍵影響因數\<資料行 >**。 您可以自訂此報表，如下列程序所述。  
  
#### <a name="create-a-custom-report"></a>建立自訂報表  
  
1.  在**根據關鍵影響因數的辨識**對話方塊方塊中，選擇您想要從選取比較的兩個值**值 1**和**值 2**下拉式清單中. 例如，您可能比較買主與非買主。  
  
2.  按一下**將報表加入**。  
  
     此精靈會建立新的工作表，並加入每一對關鍵因數比較的資料表。  
  
3.  當您完成比較之後時，按一下**關閉**。  
  
## <a name="understanding-the-key-influencers-report"></a>了解關鍵影響因數報表  
 建立資料模型之後，**分析關鍵影響因數**工具會建立報表，協助您瀏覽和比較關鍵影響因數。  
  
-   左邊的報表是預設產生的報表。 其中會顯示結果資料行的最強預測指標 (相依變數)。  
  
-   右邊的報表是選擇性的，您可以藉由比較兩個特定的結果值建立該報表。 這個報表會比較購買者與非購買者。  
  
-   請注意，針對您建立的每個報表會加入一個新的工作表。 您可以在資料表建立之後移動資料表；我們會將它們並排放置以進行比較。  
  
 ![DM13](media/dm13-tat-aki-report.gif "DM13")  
  
 **相對影響**  
 第一個報表中的陰影垂直線表示此屬性與結果之間關聯的強度。  
  
 此垂直線的長度表示此因數造成結果發生的機率；因此，當陰影垂直線越長，就表示關聯性越強。  
  
 **喜好**  
 在第二個報表中，您比較的目標值會列在兩個資料行中，其中相關因素會依照信心的遞減順序列出。  
  
-   **藍色**垂直線顯示影響結果，「 否 」 的屬性 (= 未購買)。  
  
-   **紅色**列會顯示屬性影響結果，「 是 」 (= 購買自行車)。  
  
 陰影垂直線會使用任意色彩。 您可以透過在 Excel 中設定資料表設計的選項變更這些色彩。  
  
 在比較兩個值的報表中，第二份報表會根據對目標值的影響數量來排名關鍵影響因數。  
  
 由於所有圖表都是以 Excel 資料表為基礎，因此您可以篩選及排序，以強調特定因數或結果。  
  
## <a name="more-about-the-analyze-key-influencers-tool"></a>進一步了解分析關鍵影響因數工具  
 當**分析關鍵影響因數**工具會分析您的資料，它會進行下列作業：  
  
-   建立資料結構來儲存與資料分佈有關的重要資訊。  
  
-   使用 Microsoft 貝氏機率分類演算法來建立模型。  
  
-   建立將每個資料行的資料與所指定結果產生關聯的預測。  
  
-   使用每個預測的信心分數識別產生目標結果的最具影響力因數。  
  
-   建立報表，描述依信心分數排序的關鍵影響因數。  
  
### <a name="requirements"></a>需求  
 如果目標資料行包含連續的數值，此工具會自動將這些數值分割成若干群組， 這些群組代表具有類似特性之案例的群集。 但是，數值可能會分成若干使用者易記的群組。 例如，報表可能包含的群組，例如"\<12.85701"，而報表使用者通常會喜歡看到使用整數的數字，例如 10-19、 20-29 等等。  
  
 如果您想要以不同的方式來分組數值資料，您必須在建立分析之前，先以您想要的方式分割資料。 例如，您可以使用[重定標籤](relabel-sql-server-data-mining-add-ins.md)for Excel，才能在個別的資料行，建立新的群組標籤，然後在分析中使用該新資料行的資料採礦用戶端工具。  
  
### <a name="related-tools"></a>相關工具  
 **資料採礦**功能區所提供更進階的工具，包括自訂資料採礦模型的能力  
  
 如果您使用儲存您的模型**分析關鍵影響因數**工具，您可以使用資料採礦用戶端瀏覽模型，並探索更多詳細資料中的關聯性。 如需資訊，請參閱[Excel 中瀏覽模型&#40;SQL Server 資料採礦增益集&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)。 您也可以使用 Microsoft Office Visio 來建立圖表，以群集或相依性網路的形式顯示關聯性。 如需詳細資訊，請參閱[疑難排解 Visio 資料採礦圖表&#40;SQL Server 資料採礦增益集&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)。  
  
> [!NOTE]  
>  當您關閉工作表或結束與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器的連接時，使用資料表分析工具所建立的模型會被刪除。 因此，只能在連接保持開啟時瀏覽模型。 如果您關閉連接或關閉工作表，就無法在 Visio 中轉譯模型。  
  
 如需有關所使用的演算法**分析關鍵影響因數**工具，請參閱 < Microsoft 貝氏機率分類演算法 」 SQL Server 線上叢書 》 中。  
  
## <a name="see-also"></a>另請參閱  
 [適用於 Excel 的資料表分析工具](table-analysis-tools-for-excel.md)   
 [建立資料採礦模型](creating-a-data-mining-model.md)  
  
  