---
title: 轉換 Oracle 架構（OracleToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Conversion Results
ms.assetid: e021182d-31da-443d-b110-937f5db27272
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 638c16de8312456410c14e38fa632085e504913e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68266146"
---
# <a name="converting-oracle-schemas-oracletosql"></a>轉換 Oracle 結構描述 (OracleToSQL)
當您連接到 Oracle、連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]並設定專案和資料對應選項之後，就可以將 Oracle 資料庫物件轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫物件。  
  
## <a name="the-conversion-process"></a>轉換程式  
轉換資料庫物件會從 Oracle 取得物件定義、將其轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]類似的物件，然後將此資訊載入至 SSMA 中繼資料。 它不會將資訊載入的實例中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 接著，您可以使用 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料瀏覽器] 來查看物件及其屬性。  
  
在轉換期間，SSMA 會將輸出訊息列印到 [輸出] 窗格，並在 [錯誤清單] 窗格中顯示錯誤訊息。 使用輸出和錯誤資訊來判斷您是否必須修改 Oracle 資料庫或轉換程式，以取得所需的轉換結果。  
  
## <a name="setting-conversion-options"></a>設定轉換選項  
在轉換物件之前，請先查看 [**專案設定**] 對話方塊中的 [專案轉換] 選項。 藉由使用此對話方塊，您可以設定 SSMA 如何轉換函式和全域變數。 如需詳細資訊，請參閱[&#40;轉換&#41; &#40;OracleToSQL&#41;的專案設定](../../ssma/oracle/project-settings-conversion-oracletosql.md)。  
  
## <a name="conversion-results"></a>轉換結果  
下表顯示轉換的 Oracle 物件，以及產生[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的物件：  
  
|||  
|-|-|  
|Oracle 物件|產生 SQL Server 物件|  
|函式|如果函式可以直接轉換成[!INCLUDE[tsql](../../includes/tsql-md.md)]，則 SSMA 會建立函式。<br /><br />在某些情況下，函數必須轉換成預存程式。 在此情況下，SSMA 會建立一個預存程式，以及一個呼叫預存程式的函數。|  
|程序|如果程式可以直接轉換成[!INCLUDE[tsql](../../includes/tsql-md.md)]，則 SSMA 會建立預存程式。<br /><br />在某些情況下，必須在自發交易中呼叫預存程式。 在此情況下，SSMA 會建立兩個預存程式：一個用來執行程式，另一個則用來呼叫執行預存程式。|  
|Packages|SSMA 會建立一組預存程式和函式，並透過類似的物件名稱進行整合。|  
|序列|SSMA 會建立順序物件（SQL Server 2012 或 SQL Server 2014）或模擬 Oracle 序列。|  
|具有相依物件（例如索引和觸發程式）的資料表|SSMA 會建立具有相依物件的資料表。|  
|具有相依物件的視圖，例如觸發程式|SSMA 會建立具有相依物件的 views。|  
|具體化視圖|**SSMA 會在 SQL server 上建立索引的視圖，但有一些例外狀況。如果具體化視圖包含下列一或多個結構，轉換就會失敗：**<br /><br />使用者定義函數<br /><br />SELECT、WHERE 或 GROUP BY 子句中的不具決定性的欄位/函數/運算式<br /><br />SELECT *、WHERE 或 GROUP BY 子句中的 Float 資料行使用方式（先前問題的特殊案例）<br /><br />自訂資料類型（包括 nested 資料表）<br /><br />計數（相異&lt;欄位&gt;）<br /><br />FETCH<br /><br />OUTER 聯結 (LEFT、RIGHT 或 FULL)<br /><br />子查詢，其他視圖<br /><br />OVER、RANK、LEAD、LOG<br /><br />MIN、MAX<br /><br />UNION、減號、INTERSECT<br /><br />HAVING|  
|觸發程序|**SSMA 會根據下列規則建立觸發程式：**<br /><br />觸發程式轉換成 INSTEAD of 觸發程式之前。<br /><br />AFTER 觸發程式會轉換成 AFTER 觸發程式。<br /><br />INSTEAD of 觸發程式會轉換成 INSTEAD of 觸發程式。 在相同作業上定義的多個 INSTEAD of 觸發程式會合並成一個觸發程式。<br /><br />資料列層級觸發程式是使用資料指標來模擬。<br /><br />串聯式觸發程式會轉換成多個個別的觸發程式。|  
|同義字|**同義字是針對下列物件類型所建立：**<br /><br />資料表和物件資料表<br /><br />視圖和物件檢視<br /><br />預存程序<br /><br />函式<br /><br />**下列物件的同義字會解析並由直接物件參考取代：**<br /><br />序列<br /><br />Packages<br /><br />JAVA 類別架構物件<br /><br />使用者定義物件類型<br /><br />另一個同義字的同義字無法遷移，而且將會標示為錯誤。<br /><br />不會針對具體化視圖建立同義字。|  
|使用者定義型別|**SSMA 不支援使用者定義類型的轉換。使用者定義型別，包括其在 PL/SQL 程式中的使用方式，會以下列規則引導的特殊轉換錯誤來標示：**<br /><br />使用者定義類型的資料表資料行會轉換成 VARCHAR （8000）。<br /><br />預存程式或函數的使用者定義型別引數會轉換成 VARCHAR （8000）。<br /><br />PL/SQL 區塊中使用者定義類型的變數會轉換成 VARCHAR （8000）。<br /><br />物件資料表會轉換成標準資料表。<br /><br />物件檢視會轉換成標準的視圖。|  
  
## <a name="converting-oracle-database-objects"></a>轉換 Oracle Database 物件  
若要轉換 Oracle 資料庫物件，請先選取您想要轉換的物件，然後讓 SSMA 執行轉換。 若要在轉換期間查看輸出訊息，請在 [ **view** ] 功能表上選取 [**輸出**]。  
  
**若要將 Oracle 物件轉換成 SQL Server 語法**  
  
1.  在 [Oracle 中繼資料 Explorer] 中，展開 Oracle 伺服器，然後展開 [**架構**]。  
  
2.  選取要轉換的物件：  
  
    -   若要轉換所有架構，請選取 [**架構**] 旁的核取方塊。  
  
    -   若要轉換或省略資料庫，請選取架構名稱旁的核取方塊。  
  
    -   若要轉換或省略物件的類別目錄，請展開架構，然後選取或清除類別旁的核取方塊。  
  
    -   若要轉換或省略個別物件，請展開 [類別目錄] 資料夾，然後選取或清除物件旁的核取方塊。  
  
3.  若要轉換所有選取的物件，以滑鼠右鍵按一下 [**架構**]，然後選取 [**轉換架構**]。  
  
    您也可以用滑鼠右鍵按一下物件或其父資料夾，然後選取 [**轉換架構**]，來轉換個別物件或物件類別。  
  
## <a name="viewing-conversion-problems"></a>流覽轉換問題  
某些 Oracle 物件可能無法轉換。 您可以藉由查看摘要轉換報告來判斷轉換成功率。  
  
**若要查看摘要報表**  
  
1.  在 [Oracle 中繼資料 Explorer] 中，選取 [**架構**]。  
  
2.  在右窗格中，選取 [**報表**] 索引標籤。  
  
    此報告會顯示已評估或轉換之所有資料庫物件的摘要評量報告。 您也可以查看個別物件的摘要報告：  
  
    -   若要查看個別架構的報表，請在 [Oracle 中繼資料瀏覽器] 中選取架構。  
  
    -   若要查看個別物件的報表，請在 [Oracle 中繼資料瀏覽器] 中選取物件。 具有轉換問題的物件會有紅色錯誤圖示。  
  
針對轉換失敗的物件，您可以查看導致轉換失敗的語法。  
  
**若要查看個別轉換問題**  
  
1.  在 [Oracle 中繼資料 Explorer] 中，展開 [**架構**]。  
  
2.  展開顯示紅色錯誤圖示的架構。  
  
3.  在架構底下，展開具有紅色錯誤圖示的資料夾。  
  
4.  選取具有紅色錯誤圖示的物件。  
  
5.  在右窗格中，按一下 [**報表**] 索引標籤。  
  
6.  在 [**報表**] 索引標籤的頂端是下拉式清單。 如果清單顯示**統計資料**，請將選取範圍變更為 [**來源**]。  
  
    SSMA 會在程式碼的正上方顯示原始程式碼和數個按鈕。  
  
7.  按一下 [**下一個問題]** 按鈕。 這是紅色錯誤圖示，其中有指向右側的箭號。  
  
    SSMA 會反白顯示它在目前物件中找到的第一個有問題的原始碼。  
  
針對每個無法轉換的專案，您必須決定要如何處理該物件：  
  
-   您可以在 [ **SQL** ] 索引標籤上修改程式的原始程式碼。  
  
-   您可以修改 Oracle 資料庫中的物件，以移除或修改有問題的程式碼。 若要將更新的程式碼載入至 SSMA，您必須更新中繼資料。 如需詳細資訊，請參閱[連接到 Oracle Database &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)。  
  
-   您可以從遷移中排除物件。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [中繼資料瀏覽器] 和 [Oracle 中繼資料 explorer] 中，清除專案旁的複選[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]框，然後再將物件載入並從 Oracle 遷移資料。  
  
## <a name="next-step"></a>後續步驟  
遷移程式的下一個步驟是將已[轉換的物件載入 SQL Server](loading-converted-database-objects-into-sql-server-oracletosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[將 Oracle 資料庫移轉至 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
