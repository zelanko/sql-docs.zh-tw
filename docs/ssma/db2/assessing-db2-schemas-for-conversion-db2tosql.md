---
title: 評估 DB2 架構的轉換（DB2ToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8892f5a4-72ba-4406-8649-7a9d67f4c1d9
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 506b9a32b465c9006fe4030bd6fcbb8ba4d0f136
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67938332"
---
# <a name="assessing-db2-schemas-for-conversion-db2tosql"></a>評估 DB2 架構的轉換（DB2ToSQL）
在您載入物件並將資料移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]至之前，您應該決定遷移的複雜程度，以及遷移所需的時間。 SSMA 可以建立評量報告，以顯示將成功轉換的物件百分比。 SSMA 也可讓您查看導致轉換失敗的特定問題。  
  
## <a name="creating-assessment-reports"></a>建立評量報告  
當它建立此評量報告時，SSMA 會將選取的 DB2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫物件轉換成語法，然後顯示結果。  
  
**若要建立評量報告**  
  
1.  在 DB2 Metadata Explorer 中，選取要評估的架構。  
  
2.  若要省略個別物件，請清除這些物件旁的核取方塊。  
  
3.  以滑鼠右鍵按一下 [**架構**]，然後選取 [**建立報表**]。  
  
    您也可以用滑鼠右鍵按一下物件，然後選取 [**建立報表**]，來分析個別物件。  
  
    SSMA 會在視窗底部的狀態列中顯示進度。 如果顯示 [輸出] 窗格，您也會在 [輸出] 窗格中看到訊息。  
  
    當評估完成時，將會[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]顯示 [DB2：評估報告] 視窗的 [移轉小幫手]。  
  
## <a name="using-assessment-reports"></a>使用評量報告  
[評量報告] 視窗包含三個窗格：  
  
-   左窗格包含評量報告中包含的物件階層。 您可以流覽階層，並選取物件和物件類別，以查看轉換統計資料和程式碼。  
  
-   右窗格的內容取決於在左窗格中選取的專案。  
  
    如果選取了一組物件（例如架構），或選取了資料表，右窗格就會包含 [轉換統計資料] 窗格和 [依類別目錄的物件] 窗格。 [轉換統計資料] 窗格會顯示所選物件的轉換統計資料。 [依類別目錄的物件] 窗格會顯示物件或物件類別的轉換統計資料。  
  
    如果選取了 [函式]、[封裝]、[程式]、[順序] 或 [視圖]，右窗格會包含統計資料、原始程式碼和目的程式代碼。  
  
    -   最上層的區域會顯示物件的整體統計資料。 您可能必須展開 [**統計資料]** 以查看此資訊。  
  
    -   [來源] 區域會顯示在左窗格中選取之物件的原始程式碼。 反白顯示的區域會顯示有問題的原始程式碼。  
  
    -   目的地區域會顯示轉換後的程式碼。 紅色文字會顯示有問題的程式碼和錯誤訊息。  
  
-   底部窗格會顯示以訊息編號分組的轉換訊息。 您可以按一下 [**錯誤**]、[**警告**] 或 [**資訊**] 來查看訊息的類別，然後展開一組訊息。 按一下個別訊息，在左窗格中選取物件，並在右窗格中顯示詳細資料。  
  
## <a name="analyzing-conversion-problems-by-using-the-assessment-report"></a>使用評量報告來分析轉換問題  
[轉換統計資料] 窗格會顯示轉換統計資料。 如果任何分類的百分比小於100百分比，您應該判斷轉換失敗的原因。  
  
**若要查看轉換問題**  
  
1.  使用上一個程式中的指示來建立評量報告。  
  
2.  在左窗格中，展開具有紅色錯誤圖示的架構或資料夾。 繼續展開專案，直到您選取轉換失敗的個別專案為止。  
  
3.  在 [來源] 窗格頂端，按一下 **[下一個問題]**。  
  
    有問題的程式碼會反白顯示，如同目標流覽窗格中的相關程式碼。  
  
4.  請檢查任何錯誤訊息，然後判斷您想要對導致轉換問題的物件採取什麼動作：  
  
    -   更新 SSMA 中的 DB2 語法。 您可以更新程式、函數、觸發程式、封裝函式和封裝程式的語法。 若要更新語法，請在 [DB2 中繼資料瀏覽器] 窗格中選取物件，按一下 [ **SQL** ] 索引標籤，然後修改 SQL 程式碼。 當您離開此專案時，系統會提示您儲存已更新的語法。 您可以在 [**報表**] 索引標籤上，查看物件的回報錯誤。  
  
    -   在 DB2 中，您可以修改 DB2 物件，以移除或修改有問題的程式碼。 若要將更新的程式碼載入至 SSMA，您必須更新中繼資料。 如需詳細資訊，請參閱[連接到 DB2 資料庫 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)。  
  
    -   您可以從遷移中排除物件。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [中繼資料 explorer] 和 [Db2 中繼資料 explorer] 中，清除專案旁的核取方塊， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]然後再將物件載入並從 DB2 遷移資料。  
  
## <a name="next-step"></a>後續步驟  
[將 DB2 架構轉換 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 DB2 資料庫移轉至 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
