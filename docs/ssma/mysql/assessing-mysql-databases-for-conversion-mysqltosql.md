---
title: 評定 MySQL 資料庫的轉換 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Assessment reports
ms.assetid: 2a56a003-3b0f-453a-963c-00c9e40933ec
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: ae9210444311267569d5f240d40252d4fe024877
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139211"
---
# <a name="assessing-mysql-databases-for-conversion-mysqltosql"></a>評定 MySQL 資料庫的轉換 (MySQLToSQL)
在您載入的物件，並將資料移轉至之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，您應該判斷複雜移轉將會和多少時間的移轉。 SSMA 可以建立顯示的會成功轉換的物件百分比的評定報告。 SSMA 也可讓您檢視導致轉換失敗的特定問題。  
  
## <a name="creating-assessment-reports"></a>建立評定報表  
當它會建立此評定報告時，SSMA 會將轉換至選取的 MySQL 資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 的語法，然後顯示結果。  
  
**若要建立的評估報告**  
  
1.  在 [MySQL 中繼資料總管] 中，選取要評估的結構描述。  
  
2.  若要省略個別物件，請清除旁邊的核取方塊。  
  
3.  以滑鼠右鍵按一下**結構描述**，然後選取**建立報表**。  
  
    以滑鼠右鍵按一下要分析的個別物件的物件。 然後，選取**建立報表**。  
  
    SSMA 會顯示在視窗底部的 [狀態] 列中的進度。 如果 [輸出] 窗格為可見，您也會看到 [輸出] 窗格中的訊息。  
  
    當評估完成時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for MySQL，評估報告 視窗會出現。  
  
## <a name="using-assessment-reports"></a>使用評估報告  
評定報告視窗包含三個窗格：  
  
-   左的窗格包含評估報告中包含的物件的階層。 您可以瀏覽階層，並選取物件和類別目錄的物件，若要檢視轉換統計資料和程式碼。  
  
-   右窗格的內容取決於選取的左窗格中的項目。  
  
    如果已選取的一組物件，例如結構描述，右窗格就會包含類別目錄 窗格的轉換統計資料 窗格和物件。 轉換統計資料 窗格會顯示所選物件的轉換統計資料。 依分類 窗格中的物件顯示的物件或類別目錄的物件轉換統計資料。  
  
    如果選取的函式、 程序、 資料表或檢視時，右窗格會包含統計資料、 來源和目標的程式碼。  
  
    -   最上層區域會顯示物件的整體統計資料。 您可能必須展開**統計資料**若要檢視這項資訊。  
  
    -   來源區域會顯示與所選物件的左窗格中的原始程式碼。 反白顯示的區域會顯示有問題的原始程式碼。  
  
    -   目標區域會顯示轉換後的程式碼。 紅色文字顯示有問題的程式碼和錯誤訊息。  
  
-   下方窗格會顯示轉換訊息，依訊息數目。 您可以按一下**錯誤**，**警告**，或**資訊**來檢視類別的訊息，然後再展開 一組訊息。 按一下左窗格中選取物件，然後在右窗格中顯示詳細資料的個別訊息。  
  
## <a name="analyzing-conversion-problems-by-using-the-assessment-report"></a>使用評估報告分析轉換問題  
轉換統計資料 窗格會顯示轉換統計資料。 如果任何類別目錄的百分比是小於 100%，您應該判斷為什麼轉換不成功。  
  
**若要檢視轉換的問題**  
  
1.  使用先前程序中的指示，以建立評量報告。  
  
2.  在左窗格中，展開 結構描述或有紅色錯誤圖示的資料夾。 繼續展開項目，直到您選取轉換失敗的個別項目。  
  
3.  在 [來源] 窗格頂端，按一下**下一個問題**。  
  
    有問題的程式碼會反白顯示，因為相關的程式碼的目標導覽窗格中。  
  
4.  檢閱任何錯誤訊息，並決定 要如何處理該物件造成轉換問題。  
  
-   更新在 SSMA 中的 MySQL 語法。 您可以更新僅適用於程序和函式的語法。 若要更新的語法，在 MySQL 中繼資料總管] 窗格中選取的物件，請按一下**SQL**索引標籤，然後修改 [SQL 程式碼。 當您離開此項目時，系統會提示您儲存更新的語法。 您可以檢視物件回報的錯誤**報表** 索引標籤。  
  
-   在 MySQL，您可以修改 MySQL 物件，以移除或修改有問題的程式碼。 若要更新的程式碼載入 SSMA 中，您必須更新的中繼資料。 如需詳細資訊，請參閱 <<c0> [ 連接至 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)。</c0>  
  
-   您可以從移轉排除的物件。 在 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 中繼資料總管和 MySQL 中繼資料總管]，請載入到物件之前清除項目旁的核取方塊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 並將資料從 MySQL 移轉。  
  
## <a name="next-step"></a>下一個步驟  
[轉換 MySQL 資料庫&#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>另請參閱  
[移轉 MySQL 資料庫到 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
