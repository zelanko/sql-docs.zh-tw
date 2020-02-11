---
title: 轉換 Sybase ASE 資料庫物件（SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Converting Database Objects
ms.assetid: 509cb65d-2f54-427a-83d7-37919cc4e3e3
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 507ac2a61043260435a18c90fb473130988e7f35
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948518"
---
# <a name="converting-sap-ase-database-objects-sybasetosql"></a>轉換 SAP ASE 資料庫物件（SybaseToSQL）
連線到 SAP 調適型伺服器企業版（ASE）並聯機至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 azure sql 並設定專案和資料對應選項之後，您可以將 SAP 調適型伺服器 ENTERPRISE （ase） [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫物件轉換成或 azure SQL database 物件。  
  
## <a name="the-conversion-process"></a>轉換程式  
轉換資料庫物件會從 ASE 取得物件定義、將其轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]類似或 SQL Azure 物件，然後將此資訊載入至 SSMA 中繼資料。 它不會將資訊載入至的實例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL。 接著，您可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL 中繼資料瀏覽器來查看物件及其屬性。
  
在轉換期間，SSMA 會將輸出訊息列印到 [輸出] 窗格，並在 [**錯誤清單**] 窗格中顯示錯誤訊息。 使用輸出和錯誤資訊來判斷您是否必須修改 ASE 資料庫或轉換程式，以取得所需的轉換結果。  
  
## <a name="setting-conversion-options"></a>設定轉換選項  
在轉換物件之前，請先查看 [**專案設定**] 對話方塊中的 [專案轉換] 選項。 藉由使用此對話方塊，您可以設定 SSMA 如何轉換函式和全域變數。 如需詳細資訊，請參閱[&#40;轉換&#41; &#40;SybaseToSQL&#41;的專案設定](../../ssma/sybase/project-settings-conversion-sybasetosql.md)。  
  
## <a name="converting-ase-database-objects"></a>轉換 ASE 資料庫物件  
若要轉換 ASE 資料庫物件，請先選取您要轉換的物件，然後讓 SSMA 執行轉換。 若要在轉換期間查看輸出訊息，請在 [ **view** ] 功能表上選取 [**輸出**]。  
  
**將 ASE 物件轉換成 SQL Server 或 SQL Azure 語法**  
  
1.  在 [Sybase Metadata Explorer] 中，展開 ASE 伺服器，然後展開 [**資料庫**]。  
  
2.  選取要轉換的物件：  
  
    -   若要轉換所有資料庫，請選取 [**資料庫**] 旁的核取方塊。  
  
    -   若要轉換或省略資料庫，請選取或清除資料庫名稱旁邊的核取方塊。  
  
    -   若要轉換或略過個別的架構，請展開資料庫，展開 [**架構**]，然後選取或清除架構旁邊的核取方塊。  
  
    -   若要轉換或省略物件的類別目錄，請展開架構，然後選取或清除類別旁的核取方塊。  
  
    -   若要轉換或省略個別物件，請展開 [類別目錄] 資料夾，然後選取或清除物件旁的核取方塊。  
  
3.  若要轉換所有選取的物件，請以滑鼠右鍵按一下 [**資料庫**]，然後選取 [**轉換架構**]。  
  
    您也可以用滑鼠右鍵按一下物件或其包含的資料夾，然後選取 [**轉換架構**]，來轉換物件的個別物件或類別。  
  
> [!NOTE]  
> 某些 SAP ASE 系統函數並不完全符合行為中的對等 SQL Server 系統函數。 為了模擬 SAP ASE 行為，SSMA 會在已轉換的 SQL Server 資料庫中，于名為2ss 的架構下產生使用者定義的函數。 根據專案設定，部分 SQL Server 系統函數會取代為這些模擬函數。 SSMA 會建立下列使用者定義函數：  
  
||||  
|-|-|-|  
|**char_length_Nvarchar**|**index_colorder**|**ssma_datepart**|  
|**char_length_Varchar**|**inttohex**|**substring_Nvarchar**|  
|**charindex_Nvarchar**|**ssma_datediff**|**substring_Varbinary**|  
|**charindex_Varchar**|**hextoint**|**substring_Varchar**|  
|**ulowsurr**|**to_unichar**|**ssma_current_time**|  
|**uhighsurr**|||  
  
## <a name="objects-not-supported-in-azure-sql"></a>Azure SQL 中不支援的物件  
SSMA for SAP ASE 會在轉換至內部部署 SQL Server 時使用下列 T-sql 關鍵字，但 SQL Azure T-sql 語法不支援這些關鍵字：  
  
||||  
|-|-|-|  
|CHECKPOINT|CREATE/ALTER/DROP DEFAULT|CREATE/DROP RULE|  
|DBCC TRACEOFF|DBCC TRACEON|GRANT/REVOKE/DENY ALL|  
|KILL|READTEXT|SELECT INTO|  
|SET OFFSETS|SETUSER|SHUTDOWN|  
|WRITETEXT|||  
  
## <a name="viewing-conversion-problems"></a>流覽轉換問題  
某些 SAP ASE 物件可能無法轉換。 您可以藉由查看摘要轉換報告來判斷轉換成功率。  
  
**若要查看摘要報表**  
  
1.  在 [Sybase Metadata Explorer] 中，選取 [**資料庫**]。  
  
2.  在右窗格中，選取 [**報表**] 索引標籤。  
  
    此報告會顯示已評估或轉換之所有資料庫物件的摘要評量報告。 您也可以查看個別物件的摘要報告：  
  
    -   若要查看個別資料庫的報表，請在 [Sybase 中繼資料瀏覽器] 中選取資料庫。  
  
    -   若要查看個別資料庫物件的報表，請在 [Sybase Metadata Explorer] 中選取物件。 具有轉換問題的物件會有紅色錯誤圖示。  
  
針對轉換失敗的物件，您可以查看導致轉換失敗的語法。  
  
**若要查看個別轉換問題**  
  
1.  在 [Sybase Metadata Explorer] 中，展開 [**資料庫**]。  
  
2.  展開顯示紅色錯誤圖示的資料庫。  
  
3.  展開 [**架構**] 資料夾，然後展開顯示紅色錯誤圖示的架構。  
  
4.  在架構底下，展開具有紅色錯誤圖示的資料夾。  
  
5.  選取具有紅色錯誤圖示的物件。  
  
6.  在右窗格中，選取 [**報表**] 索引標籤。  
  
7.  在 [**報表**] 索引標籤的頂端是下拉式清單。 如果清單顯示**統計資料**，請將選取範圍變更為 [**來源**]。  
  
    SSMA 會在程式碼的正上方顯示原始程式碼和數個按鈕。  
  
8.  選取 **[下一個問題]**，紅色錯誤圖示，其中箭號指向右側。  
  
    SSMA for SAP ASE 會反白顯示它在目前物件中找到的第一個有問題的原始碼。  
  
針對每個無法轉換的專案，您必須決定要如何處理該物件：  
  
-   您可以在 [ **SQL** ] 索引標籤上編輯程式和觸發程式的原始程式碼。  
  
-   您可以變更 SAP ASE 物件，以移除或修改有問題的程式碼。 若要將更新的程式碼載入至 SSMA，您必須更新中繼資料。 如需詳細資訊，請參閱[連接到 SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)。  
  
-   您可以從遷移中排除物件。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure Sql 中繼資料 Explorer 和 Sybase 中繼資料瀏覽器中，清除專案旁的核取方塊，然後再[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]將物件載入或 Azure SQL，並從 SAP ASE 遷移資料。  
  
## <a name="next-steps"></a>後續步驟  
遷移程式的下一個步驟是將[轉換的資料庫物件載入 SQL Server/SQL Azure （SybaseToSQL）](https://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06)中。  
  
## <a name="see-also"></a>另請參閱  
[將 SAP ASE 資料庫移轉至 SQL Server Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
