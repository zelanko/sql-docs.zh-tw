---
title: 轉換 MySQL 資料庫（MySQLToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ac21850b-fb32-4704-9985-5759b7c688c7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1ad4cbbdf80422f87c850c44e47f82899de4c82a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68103054"
---
# <a name="converting-mysql-databases-mysqltosql"></a>轉換 MySQL 資料庫 (MySQLToSQL)
連接到 MySQL、連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 sql azure，以及設定專案和資料對應選項之後，您可以將 mysql 資料庫物件轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 sql azure 資料庫物件。  
  
## <a name="the-conversion-process"></a>轉換程式  
轉換資料庫物件會從 MySQL 取得物件定義、將其轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]類似或 SQL Azure 物件，然後將此資訊載入至 SSMA 中繼資料。 它不會將資訊載入的實例中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 接著，您可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 中繼資料瀏覽器來查看物件及其屬性。  
  
在轉換期間，SSMA 會將輸出訊息列印到 [輸出] 窗格，並在 [錯誤清單] 窗格中顯示錯誤訊息。 使用輸出和錯誤資訊來判斷您是否必須修改 MySQL 資料庫或轉換程式，以取得所需的轉換結果。  
  
## <a name="setting-conversion-options"></a>設定轉換選項  
在轉換物件之前，請先查看 [**專案設定**] 對話方塊中的 [專案轉換] 選項。 藉由使用此對話方塊，您可以設定 SSMA 如何轉換資料表和索引。 如需詳細資訊，請參閱[專案設定 &#40;轉換&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
## <a name="conversion-results"></a>轉換結果  
下表顯示轉換的 MySQL 物件，以及產生[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的物件：  
  
|||  
|-|-|  
|**MySQL 物件**|**產生 SQL Server 物件**|  
|具有相依物件（例如索引）的資料表|SSMA 會建立具有相依物件的資料表。 資料表會以所有索引和條件約束進行轉換。 索引會轉換成不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的物件。<br /><br />**空間資料類型對應**只能在資料表節點層級執行。<br /><br />如需資料表轉換設定的詳細資訊，請參閱[轉換設定](conversion-settings-mysqltosql.md)|  
|函式|如果函式可以直接轉換成 Transact-sql，SSMA 就會建立一個函數。 在某些情況下，函數必須轉換成預存程式。 您可以使用專案設定中的函式轉換來完成這項**工作**。 在此情況下，SSMA 會建立一個預存程式，以及一個呼叫預存程式的函數。<br /><br />**提供的選擇：**<br /><br />根據專案設定進行轉換<br /><br />轉換成函式<br /><br />轉換為預存程式<br /><br />如需函數轉換設定的詳細資訊，請參閱[轉換設定](conversion-settings-mysqltosql.md)|  
|程序|如果程式可以直接轉換為 Transact-sql，SSMA 會建立預存程式。 在某些情況下，必須在自發交易中呼叫預存程式。 在此情況下，SSMA 會建立兩個預存程式：一個用來執行程式，另一個則用來呼叫執行預存程式。|  
|資料庫轉換|SSMA for MySQL 不會直接轉換作為 MySQL 物件的資料庫。 MySQL 資料庫的處理方式比較類似架構名稱，而且所有實體參數在轉換期間都會遺失。 適用于 MySQL 的 SSMA 會使用將[Mysql 資料庫對應至 SQL Server 架構 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md) ，將物件從 MySQL 資料庫對應到適當的 SQL Server 資料庫/架構配對。|  
|觸發程式轉換|**SSMA 會根據下列規則建立觸發程式：**<br /><br />在將觸發程式轉換成而不是 T-sql 觸發程式之前<br /><br />AFTER 觸發程式會在每個資料列有或沒有反復專案的 T-sql 觸發程式之後轉換成。|  
|視圖轉換|SSMA 會建立具有相依物件的視圖|  
|語句轉換|-每個 SQL 語句物件可能包含單一 MySQL 語句（例如 DDL、DML 和其他類型的語句）或開始 .。。結束區塊。<br />-   多重**語句轉換：開始 .。。結束區塊轉換**SQL 語句也可以包含 BEGIN .。。END 區塊，如同程式、函數或觸發程式定義中的一個。 這些區塊的轉換方式應該和轉換單一 MySQL 語句物件時相同。|  
  
## <a name="converting-mysql-database-objects"></a>轉換 MySQL 資料庫物件  
若要轉換 MySQL 資料庫物件，請先選取您想要轉換的物件，然後讓 SSMA 執行轉換。 若要在轉換期間查看輸出訊息，請在 [ **view** ] 功能表上選取 [**輸出**]。  
  
**將 MySQL 物件轉換成 SQL Server 或 SQL Azure 語法**  
  
1.  在 [MySQL Metadata Explorer] 中，展開 MySQL 伺服器，然後展開 [**資料庫**]。  
  
2.  選取要轉換的物件：  
  
    -   若要轉換所有架構，請選取 [**資料庫**] 旁的核取方塊。  
  
    -   若要轉換或省略資料庫，請選取資料庫名稱旁邊的核取方塊。  
  
    -   若要轉換或省略物件的類別目錄，請展開架構，然後選取或清除類別旁的核取方塊。  
  
    -   若要轉換或省略個別物件，請展開 [類別目錄] 資料夾，然後選取或清除物件旁的核取方塊。  
  
3.  若要轉換所有選取的物件，以滑鼠右鍵按一下 [**資料庫**]，然後選取 [**轉換架構**]。  
  
    您也可以用滑鼠右鍵按一下物件或其父資料夾，然後選取 [**轉換架構**]，來轉換個別物件或物件類別。  
  
## <a name="viewing-conversion-problems"></a>流覽轉換問題  
某些 MySQL 物件可能無法轉換。 您可以藉由查看摘要轉換報告來判斷轉換成功率。  
  
**若要查看摘要報表**  
  
1.  在 MySQL 中繼資料 Explorer 中，選取 [**資料庫**]。  
  
2.  在右窗格中，選取 [**報表**] 索引標籤。  
  
    此報告會顯示已評估或轉換之所有資料庫物件的摘要評量報告。 您也可以查看個別物件的摘要報告：  
  
    -   若要查看個別架構的報表，請在 [MySQL 中繼資料瀏覽器] 中選取資料庫。  
  
    -   若要查看個別物件的報表，請在 [MySQL 中繼資料瀏覽器] 中選取物件。 具有轉換問題的物件會有紅色錯誤圖示。  
  
針對轉換失敗的物件，您可以查看導致轉換失敗的語法。  
  
**若要查看個別轉換問題**  
  
1.  在 MySQL 中繼資料 Explorer 中，展開 [**資料庫**]。  
  
2.  展開顯示紅色錯誤圖示的資料庫。  
  
3.  在資料庫底下，展開具有紅色錯誤圖示的資料夾。  
  
4.  選取具有紅色錯誤圖示的物件。  
  
5.  在右窗格中，按一下 [**報表**] 索引標籤。  
  
6.  在 [**報表**] 索引標籤的頂端是下拉式清單。 如果清單顯示**統計資料**，請將選取範圍變更為 [**來源**]。  
  
    SSMA 會在程式碼的正上方顯示原始程式碼和數個按鈕。  
  
7.  按一下 [**下一個問題]** 按鈕。 這是紅色錯誤圖示，其中有指向右側的箭號。  
  
    SSMA 會反白顯示它在目前物件中找到的第一個有問題的原始碼。  
  
針對每個無法轉換的專案，您必須決定要如何處理該物件：  
  
-   您可以修改 MySQL 資料庫中的物件，以移除或修改有問題的程式碼。 若要將更新的程式碼載入至 SSMA，您必須更新中繼資料。 如需詳細資訊，請參閱[連接到 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   您可以從遷移中排除物件。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Sql Azure 中繼資料 Explorer 和 Mysql 中繼資料瀏覽器中，清除專案旁的核取方塊，然後再[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]將物件載入或 SQL Azure，並從 MySQL 遷移資料。  
  
## <a name="next-step"></a>後續步驟  
遷移程式的下一個步驟是將[轉換的資料庫物件載入 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/loading-converted-database-objects-into-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>另請參閱  
[將 MySQL 資料庫遷移至 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
