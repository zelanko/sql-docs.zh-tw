---
title: 估計 Wizard （適用于 Excel 的資料採礦增益集） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data modeling [data mining]
- estimation
ms.assetid: 7f2b1d5f-c9b3-4939-b35a-34ae099af15f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9b7ffc1b77d90946a119dc462da2057cf3fe4988
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081248"
---
# <a name="estimate-wizard-data-mining-add-ins-for-excel"></a>估計精靈 (適用於 Excel 的資料採礦增益集)
  ![資料採礦功能區中的估計精靈](media/dmc-estimate.gif "資料採礦功能區中的估計精靈")  
  
 **估計**的 wizard 可協助您建立估計模型。 估計模型會從資料擷取模式，並使用此模式來預測會影響結果的因數。  
  
 估計用於預測數值結果。 例如，如果目標資料行包含以百分比表示的學校學生畢業率，您可以分析可能會增加或減少畢業率的因數，例如每間學校的學生人數、師生比和教師人數等。  
  
## <a name="using-the-estimate-data-wizard"></a>使用估計資料精靈  
  
1.  在 [**資料採礦**] 功能區上，按一下 [**估計**]。  
  
2.  在 [**選取來源資料**] 對話方塊中，選取要使用的來源資料。 您可以使用 Excel**資料表**、Excel**資料範圍**或**外部資料源**中的資料。  
  
     如果使用外部資料來源，您可以建立自訂檢視或查詢，然後將其儲存為 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料來源。  
  
3.  在 [**估計**] 對話方塊中，選取**要分析**的資料行。  
  
     目標資料行必須包含連續數值資料。  
  
4.  勾選 [**輸入資料行**] 核取方塊，以選取要當做輸入使用的資料行。  
  
     這些資料行將會用來建立模式。 您應該從分析中刪除任何可能沒有用的資料行，例如識別碼或包含無關資料的資料行。  
  
5.  **估計**嚮導會為您的資料集選取最佳的演算法。 不過，您可以按一下 [**參數**] 來開啟 [**演算法參數**] 對話方塊，並設定 [advanced options]。  
  
6.  如果您的資料是數值，而且您可以使用 Microsoft 線性回歸方法，可以針對您知道（或強烈懷疑）與可預測值相關聯的任何數值資料行，核取 [**回歸輸入變數**] 方塊。  
  
     演算法接著會測試該資料行中的值，以判斷這些值是否會影響結果。 如果您不確定，請按一下 [**建議**]，演算法就會測試所有資料行，並自動偵測要當做回歸輸入變數使用的最佳值。  
  
    > [!NOTE]  
    >  需要迴歸輸入變數，才能建立估計值。 此精靈一定會根據最初資料的行程來建議最佳迴歸輸入變數； 因此，如果您不確定的話，最好接受建議的選擇。  
  
7.  在 [將**資料分割成定型集和測試集**] 頁面上，指定是否要建立一小部分的資料來進行測試。  
  
8.  在 [**完成]** 頁面上，提供新的「採礦結構」和「挖掘模式」的名稱，或接受所提供的預設名稱。  
  
9. 設定用來使用此模型的選項。  
  
    -   選取 **[流覽]** ，立即在檢視器中開啟模型。  
  
         這個圖形化檢視器可顯示相依性網路圖形以及演算法產生的決策樹。 藉由瀏覽此資訊，您可以更加了解會影響預估值的因數。  
  
    -   選取 [**啟用鑽取**]，讓您分析的使用者能夠查看基礎資料。  
  
         只有在使用決策樹 opr 線性迴歸演算法時，才可以使用此選項。  
  
    -   **使用暫時性模型**。 如果選取這個選項，此模型將無法儲存到伺服器。 當您關閉 Excel 時，即會刪除暫時性模型。  
  
## <a name="more-about-estimation-models"></a>進一步了解估計模型  
 **估計**的 wizard 支援使用下列任何一種演算法：  
  
-   Microsoft 決策樹演算法  
  
-   Microsoft 線性迴歸演算法  
  
-   Microsoft 羅吉斯迴歸演算法  
  
-   Microsoft 類神經網路演算法  
  
 在 [**演算法參數**] 對話方塊中，您可以根據您選擇的演算法，設定其他的 [其他] 選項。 如需每個演算法選項的資訊，請參閱《SQL Server 線上叢書》的下列主題：  
  
 [Microsoft 決策樹演算法技術參考](data-mining/microsoft-decision-trees-algorithm-technical-reference.md)  
  
 [Microsoft 線性迴歸演算法技術參考](data-mining/microsoft-linear-regression-algorithm-technical-reference.md)  
  
 [Microsoft 羅吉斯迴歸演算法技術參考](data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)  
  
 [Microsoft 類神經網路演算法技術參考資料](data-mining/microsoft-neural-network-algorithm-technical-reference.md)  
  
### <a name="requirements"></a>需求  
 您必須連接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫，才能使用估計資料精靈。  
  
 如需有關如何建立連線的詳細資訊，請參閱[連接到來源資料 &#40;適用于 Excel&#41;的資料採礦用戶端](connect-to-source-data-data-mining-client-for-excel.md)。  
  
 若要使用估計演算法，您嘗試預測的結果必須以數值表示，例如貨幣、銷售量、日期或時間。  
  
## <a name="see-also"></a>另請參閱  
 [建立資料採礦模型](creating-a-data-mining-model.md)   
 [決策樹圖表逐步解說 &#40;資料採礦增益集&#41;](decision-tree-diagram-walkthrough-data-mining-add-ins.md)  
  
  
