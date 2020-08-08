---
title: 評定 SAP ASE 資料庫物件的轉換 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eb996b7c-1eef-4f73-b5e6-2fa6faf7336c
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: fba4692780b9f9f2c556634bf1676bc00bbba169
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87932609"
---
# <a name="assessing-sap-ase-database-objects-for-conversion-sybasetosql"></a>評定 SAP ASE 資料庫物件的轉換 (SybaseToSQL) 
在您載入物件並將資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 AZURE SQL 之前，您應該先判斷遷移的複雜性，以及應該花多少時間。 SSMA 可以建立評量報告，以顯示將成功轉換成的物件和程式的百分比 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。 SSMA 也可讓您查看可能會導致轉換失敗的特定問題。  
  
## <a name="create-assessment-reports"></a>建立評量報告  
建立此評量報告時，SSMA 會將選取的 SAP 調適型伺服器 Enterprise (ASE) 資料庫物件轉換為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 AZURE SQL 語法，然後顯示結果。  
  
**若要建立評量報告**  
  
1.  在 [Sybase Metadata Explorer] 中，選取您想要評估的資料庫。  
  
2.  若要省略個別物件，請清除您不想要評估之物件旁的核取方塊。  
  
3.  以滑鼠右鍵按一下 [**資料庫**]，然後選取 [**建立報表**]。  
  
    您也可以用滑鼠右鍵按一下物件，然後選取 [**建立報表**]，來分析個別物件。  
  
    SSMA 會在視窗底部的狀態列中顯示進度。 如果顯示 [輸出] 窗格，您也會看到任何相關訊息。  
  
    當評估完成時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會顯示 [Sybase：評估報告] 視窗的 [移轉小幫手]。  
  
## <a name="use-assessment-reports"></a>使用評量報告  
[評量報告] 視窗包含三個窗格：  
  
-   左窗格包含評量報告中包含的物件階層。 您可以流覽階層並選取 [物件] 和 [物件類別]，以查看轉換統計資料和程式碼。  
  
-   右窗格的內容會根據在左窗格中選取的專案而有所不同。  
  
    如果 (的物件群組（例如架構) 或已選取資料表），右窗格會顯示兩個窗格。 [**轉換統計資料**] 窗格會顯示所選物件的轉換統計資料。 [**依類別目錄的物件**] 窗格會顯示物件或物件類別的轉換統計資料。  
  
    如果選取了 [預存程式]、[view] 或 [觸發程式]，右窗格會包含統計資料、原始程式碼和目的程式代碼。  
  
    -   最上層的區域會顯示物件的整體統計資料。 您可能必須展開 [**統計資料]** 以查看此資訊。 
    -   [來源] 區域會顯示在左窗格中選取之物件的原始程式碼。 反白顯示的區域會顯示有問題的原始程式碼。  
    -   目的地區域會顯示轉換後的程式碼。 紅色文字會顯示有問題的程式碼和錯誤訊息。  
  
-   底部窗格會顯示以訊息編號分組的轉換訊息。 選取 [**錯誤**]、[**警告**] 或 [**資訊**] 以查看訊息的類別，然後展開一組訊息。 按一下個別訊息，在左窗格中選取物件，然後在右窗格中顯示詳細資料。  
  
## <a name="analyze-conversion-problems-by-using-the-assessment-report"></a>使用評量報告來分析轉換問題  
[**轉換統計資料] 窗格**會顯示轉換統計資料。 如果任何分類的百分比小於100百分比，您應該判斷轉換失敗的原因。  
  
**若要查看轉換問題**  
  
1.  使用上一個程式中的指示來建立評量報告。  
  
2.  在左窗格中，展開具有紅色錯誤圖示的架構或資料夾。 繼續展開專案，直到您選取轉換失敗的個別專案為止。  
  
3.  在 [來源] 窗格的頂端，選取 **[下一個問題]**。  
    有問題的程式碼會反白顯示，如同**目標流覽**窗格中的相關程式碼。  
  
4.  請檢查任何錯誤訊息，然後判斷您想要對導致轉換問題的物件採取什麼動作：  
  
    -   更新 SSMA 中的 ASE 語法。 您只能更新預存程式和觸發程式的語法。 若要更新語法，請在 [Sybase 中繼資料瀏覽器] 窗格中選取物件，按一下 [ **sql** ] 索引標籤，然後編輯 SQL 程式碼。 當您離開此專案時，系統會提示您儲存已更新的語法。 在 [**報表**] 索引標籤上，查看物件的回報錯誤。  
  
    -   在 ASE 中，您可以改變 ASE 物件，以移除或修改有問題的程式碼。 若要將更新的程式碼載入至 SSMA，您必須更新中繼資料。 如需詳細資訊，請參閱[連接到 SYBASE ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)。  
  
    -   您可以從遷移中排除物件。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 AZURE Sql 中繼資料 explorer 和 Sybase 中繼資料瀏覽器中，清除專案旁的核取方塊，然後再將物件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL，並從 ASE 遷移資料。
  
## <a name="next-steps"></a>後續步驟  
[將 SAP ASE 資料庫物件轉換 &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 SAP ASE 資料庫移轉至 SQL Server Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
