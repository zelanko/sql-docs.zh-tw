---
description: 評定 Oracle 結構描述的轉換 (OracleToSQL)
title: 評定 Oracle 架構以進行轉換 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Analyzing Conversion Problems
ms.assetid: 4de9bcf6-1346-4740-87f9-7f24a8226357
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 641d97868dcd308dbe487d43b7eba84a8b772371
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88320734"
---
# <a name="assessing-oracle-schemas-for-conversion-oracletosql"></a>評定 Oracle 結構描述的轉換 (OracleToSQL)
在載入物件並將資料移轉至之前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您應該判斷遷移的複雜度，以及遷移將花費多少時間。 SSMA 可以建立評定報表，以顯示將成功轉換之物件的百分比。 SSMA 也可讓您查看造成轉換失敗的特定問題。  
  
## <a name="creating-assessment-reports"></a>建立評量報告  
當它建立這份評量報告時，SSMA 會將選取的 Oracle 資料庫物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 語法，然後顯示結果。  
  
**若要建立評量報告**  
  
1.  在 [Oracle 中繼資料瀏覽器] 中，選取要評估的架構。  
  
2.  若要省略個別物件，請清除這些物件旁的核取方塊。  
  
3.  以滑鼠右鍵按一下 [ **架構**]，然後選取 [ **建立報告**]。  
  
    您也可以在物件上按一下滑鼠右鍵，然後選取 [ **建立報表**]，來分析個別的物件。  
  
    SSMA 會在視窗底部的狀態列中顯示進度。 如果 [輸出] 窗格是可見的，您也會在 [輸出] 窗格中看到訊息。  
  
    評量完成時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將會出現 [Oracle：評定報表] 視窗的 Migration Assistant。  
  
## <a name="using-assessment-reports"></a>使用評量報告  
[評量報表] 視窗包含三個窗格：  
  
-   左窗格包含評量報告中所包含之物件的階層。 您可以流覽階層，並選取物件和物件類別來查看轉換統計資料和程式碼。  
  
-   右窗格的內容取決於在左窗格中選取的專案。  
  
    如果選取了一組物件（例如架構），或選取了資料表，右窗格就會包含 [轉換統計資料] 窗格和 [依類別目錄的物件] 窗格。 [轉換統計資料] 窗格會顯示所選物件的轉換統計資料。 [依類別的物件] 窗格會顯示物件或物件類別的轉換統計資料。  
  
    如果已選取 [函式]、[封裝]、[程式]、[順序] 或 [視圖]，右窗格會包含統計資料、原始程式碼和目的程式代碼。  
  
    -   上方區域會顯示物件的整體統計資料。 您可能必須展開 **統計資料** 以查看此資訊。  
  
    -   [來源] 區域會顯示在左窗格中選取之物件的原始程式碼。 反白顯示的區域會顯示有問題的原始程式碼。  
  
    -   目的地區域會顯示已轉換的程式碼。 紅色文字顯示有問題的程式碼與錯誤訊息。  
  
-   下方窗格會顯示依訊息編號分組的轉換訊息。 您可以按一下 [ **錯誤**]、[ **警告**] 或 [ **資訊** ] 來查看訊息的類別，然後展開一組訊息。 按一下個別訊息以選取左窗格中的物件，並在右窗格中顯示詳細資料。  
  
## <a name="analyzing-conversion-problems-by-using-the-assessment-report"></a>使用評量報告來分析轉換問題  
[轉換統計資料] 窗格會顯示轉換統計資料。 如果任何類別的百分比低於100%，您應該判斷轉換失敗的原因。  
  
**若要查看轉換問題**  
  
1.  使用上一個程式中的指示來建立評量報告。  
  
2.  在左窗格中，展開有紅色錯誤圖示的架構或資料夾。 繼續展開專案，直到您選取轉換失敗的個別專案為止。  
  
3.  在 [來源] 窗格的頂端，按一下 **[下一個問題]**。  
  
    會反白顯示有問題的程式碼，就像目標流覽窗格中的相關程式碼一樣。  
  
4.  檢查是否有任何錯誤訊息，然後判斷您想要如何處理造成轉換問題的物件：  
  
    -   更新 SSMA 中的 Oracle 語法。 您可以更新程式、函式、觸發程式、封裝函數和封裝程式的語法。 若要更新語法，請在 [Oracle 中繼資料瀏覽器] 窗格中選取物件，按一下 [ **sql** ] 索引標籤，然後修改 sql 程式碼。 當您離開專案時，系統會提示您儲存更新的語法。 您可以在 [ **報表** ] 索引標籤上，查看物件的回報錯誤。  
  
    -   在 Oracle 中，您可以修改 Oracle 物件來移除或修改有問題的程式碼。 若要將更新的程式碼載入至 SSMA，您必須更新中繼資料。 如需詳細資訊，請參閱 [連接到 Oracle Database &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)。  
  
    -   您可以從遷移中排除物件。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [中繼資料瀏覽器] 和 [Oracle 中繼資料瀏覽器] 中，清除專案旁的核取方塊，然後將物件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和遷移 Oracle 中的資料。  
  
## <a name="next-step"></a>後續步驟  
[&#40;OracleToSQL&#41;轉換 Oracle 架構 ](../../ssma/oracle/converting-oracle-schemas-oracletosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 Oracle 資料庫移轉至 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
