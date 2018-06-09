---
title: 將 MySQL 資料庫 (MySQLToSQL) 轉換 |Microsoft 文件
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ac21850b-fb32-4704-9985-5759b7c688c7
caps.latest.revision: 17
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 3b1f69f577a26ff0858599e9f597eac95972fcb5
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34775964"
---
# <a name="converting-mysql-databases-mysqltosql"></a>將 MySQL 資料庫 (MySQLToSQL) 轉換
您已經連接到 MySQL 之後，連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 及設定專案和對應的資料選項，您可以將轉換至的 MySQL 資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫物件。  
  
## <a name="the-conversion-process"></a>轉換程序  
轉換的資料庫物件從 MySQL 接受物件定義、 將它們轉換成類似[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 物件，然後再將這項資訊載入至 SSMA 中繼資料。 不會載入到的執行個體資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 您接著可以使用檢視物件和其屬性[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中繼資料總管。  
  
在轉換期間，SSMA 會列印至輸出窗格的輸出訊息和錯誤訊息 [錯誤清單] 窗格。 用於判斷是否需要修改您的 MySQL 資料庫或您轉換程序，以取得所需的轉換結果的輸出和錯誤的資訊。  
  
## <a name="setting-conversion-options"></a>設定轉換選項  
在轉換前的物件，請檢閱中的專案轉換選項**專案設定** 對話方塊。 藉由使用此對話方塊中，您可以設定 SSMA 如何轉換資料表和索引。 如需詳細資訊，請參閱[專案設定&#40;轉換&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
## <a name="conversion-results"></a>轉換結果  
下表顯示 MySQL 的物件轉換，並產生[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]物件：  
  
|||  
|-|-|  
|**MySQL 物件**|**產生 SQL Server 物件**|  
|具有相依的物件，例如： 索引的資料表|SSMA 會建立資料表，與相依物件。 資料表，轉換為所有索引和條件約束。 索引會轉換成個別[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]物件。<br /><br />**空間資料類型對應**可以只在資料表節點層級執行。<br /><br />如需有關資料表轉換設定的詳細資訊，請參閱[轉換設定](http://msdn.microsoft.com/en-us/f551cf6e-1575-4206-9cca-975b5b43a6b8)|  
|函數|如果函式可以直接轉換成 TRANSACT-SQL，SSMA 會建立函式。 在某些情況下，函式必須轉換成預存程序。 這可以經由使用**函式轉換**專案設定中。 在此情況下，SSMA 所建立的預存程序和函式呼叫預存程序。<br /><br />**指定的選項：**<br /><br />根據專案設定轉換<br /><br />將轉換成函式<br /><br />轉換預存程序<br /><br />如需有關轉換函式設定的詳細資訊，請參閱[轉換設定](http://msdn.microsoft.com/en-us/f551cf6e-1575-4206-9cca-975b5b43a6b8)|  
|程序|如果程序可以直接轉換成 TRANSACT-SQL，SSMA 會建立預存程序。 在某些情況下，必須在自發交易中呼叫預存程序。 在此情況下，SSMA 會建立兩個預存程序： 實作程序，和另一個則用於呼叫實作的其中一個預存程序。|  
|資料庫轉換|做為 MySQL 物件的資料庫不會直接轉換的 SSMA for MySQL。 MySQL 資料庫會被視為一個類似的結構描述名稱和實體的所有參數都都會在轉換期間遺失。 SSMA for MySQL 使用[對應至 SQL Server 結構描述的 MySQL 資料庫&#40;MySQLToSQL&#41; ](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)對應到適當的 SQL Server 資料庫/結構描述對 MySQL 資料庫中的物件。|  
|觸發程序轉換|**SSMA 會建立觸發程序根據下列規則：**<br /><br />觸發程序轉換成有 T-SQL 的 INSTEAD OF 觸發程序之前<br /><br />AFTER 觸發程序會轉換成之後 T-SQL 觸發程序，不論反覆項目，每個資料列。|  
|檢視轉換|SSMA 會建立與相依物件的檢視表|  
|陳述式轉換|-每個 SQL 陳述式物件可能包含單一 MySQL 陳述式 （例如 DDL、 DML 和其他類型的陳述式） 或開始...結束區塊。<br />-   **多重陳述式轉換： 開始...結束區塊轉換**SQL 陳述式也可以包含在 BEGIN...END 區塊，例如其中一個程序、 函數或觸發程序定義中。 要轉換的單一 MySQL 陳述式物件的相同方式，應該將這些區塊轉換。|  
  
## <a name="converting-mysql-database-objects"></a>轉換的 MySQL 資料庫物件  
若要將 MySQL 資料庫物件，您先選取您要轉換的物件，然後執行轉換的 SSMA。 若要進行轉換時，檢視輸出訊息上**檢視**功能表上，選取**輸出**。  
  
**若要將 MySQL 物件轉換成 SQL Server 或 SQL Azure 的語法**  
  
1.  在 MySQL 中繼資料總管]，展開 [MySQL server，然後展開**資料庫**。  
  
2.  選取要轉換的物件：  
  
    -   若要轉換的所有結構描述，選取核取方塊旁的 **資料庫**。  
  
    -   若要轉換或省略資料庫，選取 資料庫名稱旁邊的核取方塊。  
  
    -   轉換或省略物件的類別，結構描述中，依序展開，然後選取或清除類別旁的核取方塊。  
  
    -   轉換或省略個別物件，展開類別目錄資料夾，然後選取或清除物件旁的核取方塊。  
  
3.  若要將所有選取的物件，以滑鼠右鍵按一下**資料庫**選取**轉換結構描述**。  
  
    您也可以轉換個別物件或類別目錄的物件，該物件或其父資料夾上按一下滑鼠右鍵，然後選取**轉換結構描述**。  
  
## <a name="viewing-conversion-problems"></a>檢視轉換問題  
某些 MySQL 物件可能不會轉換。 您可以檢視摘要轉換報表來判斷轉換成功率。  
  
**若要檢視摘要報表**  
  
1.  在 MySQL 中繼資料總管，選取**資料庫**。  
  
2.  在右窗格中，選取**報表** 索引標籤。  
  
    此報告會顯示摘要評估報表中的所有資料庫物件評估或轉換。 您也可以檢視個別物件的摘要報告：  
  
    -   若要檢視報表中的個別結構描述，請在 MySQL 中繼資料總管 選取的資料庫。  
  
    -   若要檢視報表中的個別物件，請在 MySQL 中繼資料總管 選取的物件。 已轉換問題的物件具有紅色錯誤圖示。  
  
無法轉換的物件，您可以檢視導致轉換失敗的語法。  
  
**若要檢視個別轉換問題**  
  
1.  在 MySQL 中繼資料總管，依序展開**資料庫**。  
  
2.  展開會顯示紅色錯誤圖示的資料庫。  
  
3.  在資料庫中，展開一個資料夾具有紅色錯誤圖示。  
  
4.  選取具有紅色錯誤圖示的物件。  
  
5.  在右窗格中，按一下 [**報表**] 索引標籤。  
  
6.  在頂端**報表** 索引標籤是下拉式清單。 如果此清單會顯示**統計資料**，變更選取範圍到**來源**。  
  
    SSMA 會顯示與原始程式碼和數個程式碼正上方的按鈕。  
  
7.  按一下**下一個問題** 按鈕。 這是指向右側的箭號紅色錯誤圖示。  
  
    SSMA 會反白顯示在目前的物件中找到的第一個有問題的原始碼。  
  
針對無法轉換每個項目，您必須決定您想要使用該物件：  
  
-   您可以修改 MySQL 資料庫，以移除或修改有問題的程式碼中的物件。 若要更新的程式碼載入 SSMA，您必須更新的中繼資料。 如需詳細資訊，請參閱[連接至 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   您可以從移轉排除的物件。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中繼資料總管和 MySQL 中繼資料總管，清除項目旁邊的核取方塊，然後再載入物件到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 和從 MySQL 移轉資料。  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是[載入轉換的資料庫物件至 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/loading-converted-database-objects-into-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>另請參閱  
[移轉的 MySQL 資料庫到 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
