---
title: "評估 MySQL 資料庫轉換 (MySQLToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords: Assessment reports
ms.assetid: 2a56a003-3b0f-453a-963c-00c9e40933ec
caps.latest.revision: "10"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 73019709b3ce9b40dc05f678cc64d33305504213
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="assessing-mysql-databases-for-conversion-mysqltosql"></a>評估的 MySQL 資料庫轉換 (MySQLToSQL)
在您載入的物件，並將資料移轉至之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，您應該決定如何複雜移轉，以及多少時間會移轉。 SSMA 可以建立顯示成功轉換的物件百分比的評估報告。 SSMA 也可讓您檢視特定的問題，導致轉換失敗。  
  
## <a name="creating-assessment-reports"></a>建立的評估報告  
SSMA 轉換至選取的 MySQL 資料庫物件時它會建立此評估報表，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 語法，然後顯示結果。  
  
**若要建立的評估報告**  
  
1.  在 MySQL 中繼資料總管，選取要評估的結構描述。  
  
2.  若要省略個別物件，請清除旁邊的核取方塊。  
  
3.  以滑鼠右鍵按一下**結構描述**，然後選取**建立報表**。  
  
    以滑鼠右鍵按一下要分析的個別物件的物件。 然後，選取**建立報表**。  
  
    SSMA 會顯示在視窗底部的狀態列中的進度。 如果 [輸出] 窗格是可見的也會看到 [輸出] 窗格中的訊息。  
  
    當評估完成時[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]移轉小幫手的 MySQL 評估報表視窗中會出現。  
  
## <a name="using-assessment-reports"></a>使用評估報告  
評估報表視窗包含三個窗格：  
  
-   左的窗格包含評估報表中包含的物件的階層。 您可以瀏覽階層，並選取物件和類別目錄的物件，若要檢視轉換統計資料和程式碼。  
  
-   右窗格的內容取決於選取左窗格中的項目。  
  
    如果選取的物件群組，例如結構描述，在右窗格就會包含類別目錄 窗格的轉換統計資料 窗格和物件。 轉換統計資料 窗格會顯示所選物件的轉換統計資料。 依類別目錄 窗格的物件顯示的轉換統計資料物件或類別目錄的物件。  
  
    如果選取的函式、 程序、 資料表或檢視時，右窗格會包含統計資料、 原始碼和目標程式碼。  
  
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
  
4.  檢閱任何錯誤訊息，，然後決定您想要使用該物件造成轉換問題。  
  
-   更新 MySQL 語法 SSMA 中。 您可以更新僅適用於程序和函式的語法。 若要更新的語法，MySQL 中繼資料總管 窗格中選取的物件，請按一下**SQL**索引標籤，然後再修改的 SQL 程式碼。 當您離開此項目時，系統會提示您儲存更新的語法。 您可以檢視報告的錯誤物件上**報表** 索引標籤。  
  
-   在 MySQL，您可以修改 MySQL 物件，以移除或修改程式碼有問題。 若要更新的程式碼載入 SSMA，您必須更新的中繼資料。 如需詳細資訊，請參閱[連接到 MySQL &#40;MySQLToSQL &#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md).  
  
-   您可以從移轉排除的物件。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中繼資料總管和 MySQL 中繼資料總管，清除項目旁邊的核取方塊之前物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 和從 MySQL 移轉資料。  
  
## <a name="next-step"></a>下一個步驟  
[轉換的 MySQL 資料庫 &#40;MySQLToSQL &#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>請參閱  
[將 MySQL 資料庫移轉至 SQL Server-Azure SQL DB &#40;MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
