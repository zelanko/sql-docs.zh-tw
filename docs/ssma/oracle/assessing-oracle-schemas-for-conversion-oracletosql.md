---
title: "評估 Oracle 結構描述轉換 (OracleToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Analyzing Conversion Problems
ms.assetid: 4de9bcf6-1346-4740-87f9-7f24a8226357
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 03bfafd71f7e90e8f1529635fead6a7f2718314a
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="assessing-oracle-schemas-for-conversion-oracletosql"></a>轉換 (OracleToSQL) 評估 Oracle 結構描述
在您載入的物件，並將資料移轉至之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您應該決定如何複雜移轉，以及多少時間會移轉。 SSMA 可以建立顯示成功轉換的物件百分比的評估報告。 SSMA 也可讓您檢視特定的問題，導致轉換失敗。  
  
## <a name="creating-assessment-reports"></a>建立的評估報告  
SSMA 轉換至選取的 Oracle 資料庫物件時它會建立此評估報表，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]語法，然後顯示結果。  
  
**若要建立的評估報告**  
  
1.  在 Oracle 中繼資料總管，選取要評估的結構描述。  
  
2.  若要省略個別物件，請清除旁邊的核取方塊。  
  
3.  以滑鼠右鍵按一下**結構描述**，然後選取**建立報表**。  
  
    您也可以分析個別物件，以滑鼠右鍵按一下物件，然後選取**建立報表**。  
  
    SSMA 會顯示在視窗底部的狀態列中的進度。 如果 [輸出] 窗格是可見的也會看到 [輸出] 窗格中的訊息。  
  
    當評估完成時[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]移轉小幫手，Oracle： 評估報表視窗中會出現。  
  
## <a name="using-assessment-reports"></a>使用評估報告  
評估報表視窗包含三個窗格：  
  
-   左的窗格包含評估報表中包含的物件的階層。 您可以瀏覽階層，並選取物件和類別目錄的物件，若要檢視轉換統計資料和程式碼。  
  
-   在右窗格的內容取決於選取左窗格中的項目。  
  
    如果選取的物件群組，則這類結構描述，或右窗格的類別目錄 窗格選取資料表時，如果包含轉換統計資料 窗格和物件。 轉換統計資料 窗格會顯示所選物件的轉換統計資料。 依類別目錄 窗格的物件顯示的轉換統計資料物件或類別目錄的物件。  
  
    如果選取函式、 封裝、 程序、 順序或檢視時，右窗格會包含統計資料、 原始碼和目標程式碼。  
  
    -   最上層區域會顯示物件的整體統計資料。 您可能必須展開 **統計資料**若要檢視這項資訊。  
  
    -   來源區域會顯示在左窗格中選取之物件的原始程式碼。 反白顯示的區域會顯示有問題的原始程式碼。  
  
    -   目標區域會顯示轉換後的程式碼。 紅色文字顯示有問題的程式碼和錯誤訊息。  
  
-   下方窗格會顯示轉換訊息，依訊息數目。 您可以按一下**錯誤**，**警告**，或**資訊**來檢視類別的訊息，然後再展開 群組的訊息。 按一下左窗格中選取的物件，並在右窗格中顯示詳細資料的個別訊息。  
  
## <a name="analyzing-conversion-problems-by-using-the-assessment-report"></a>使用評估報表來分析轉換問題  
轉換統計資料 窗格會顯示轉換統計資料。 如果任何類別目錄的百分比是小於 100%，您應該判斷為什麼轉換不成功。  
  
**若要檢視轉換問題**  
  
1.  使用先前的程序中的指示，建立評估報表。  
  
2.  在左窗格中，展開 結構描述或有紅色錯誤圖示的資料夾。 繼續展開項目，直到您選取的轉換失敗的個別項目。  
  
3.  在 來源 窗格頂端，按一下 **下一個問題**。  
  
    有問題的程式碼會反白顯示，因為目標瀏覽窗格中的相關程式碼。  
  
4.  檢閱任何錯誤訊息，，然後決定您想要使用該物件造成轉換問題：  
  
    -   更新 SSMA 的 Oracle 語法。 您可以更新程序、 函數、 觸發程序、 函式和已封裝的程序的語法。 若要更新的語法，在 Oracle 中繼資料總管 窗格中選取的物件，請按一下**SQL**索引標籤，然後再修改的 SQL 程式碼。 當您離開此項目時，系統會提示您儲存更新的語法。 您可以檢視報告的錯誤物件上**報表** 索引標籤。  
  
    -   在 Oracle 中，您可以修改 Oracle 物件以移除或修改程式碼有問題。 若要更新的程式碼載入 SSMA，您必須更新的中繼資料。 如需詳細資訊，請參閱[連接到 Oracle 資料庫 &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)。  
  
    -   您可以從移轉排除的物件。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料總管和 Oracle 中繼資料總管，清除項目旁邊的核取方塊之前物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]並將資料從 Oracle 移轉。  
  
## <a name="next-step"></a>下一個步驟  
[轉換 Oracle 結構描述 &#40; OracleToSQL &#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 Oracle 資料庫移轉至 SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  

