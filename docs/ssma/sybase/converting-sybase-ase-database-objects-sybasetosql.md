---
title: "轉換 Sybase ASE 資料庫物件 (SybaseToSQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Converting Database Objects
ms.assetid: 509cb65d-2f54-427a-83d7-37919cc4e3e3
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: dd8fba1682d270251a865675f047e69a66e12479
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="converting-sybase-ase-database-objects-sybasetosql"></a>轉換 Sybase ASE 資料庫物件 (SybaseToSQL)
您已經連接到 Sybase Adaptive Server Enterprise (ASE) 之後，連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 及設定專案和對應的資料選項，您可以將轉換至 Sybase Adaptive Server Enterprise (ASE) 資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫物件。  
  
## <a name="the-conversion-process"></a>轉換程序  
轉換的資料庫物件會從 ASE 中取得的物件定義、 將它們轉換成類似[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 物件，然後再將這項資訊載入至 SSMA 中繼資料。 不會載入到的執行個體資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 您接著可以使用檢視物件和其屬性[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中繼資料總管。  
  
在轉換期間，SSMA 會列印至輸出窗格的輸出訊息和錯誤訊息 [錯誤清單] 窗格。 若要判斷您是否需要修改 ASE 資料庫或您要取得所需的轉換結果的轉換程序使用的輸出和錯誤的資訊。  
  
## <a name="setting-conversion-options"></a>設定轉換選項  
在轉換前的物件，請檢閱中的專案轉換選項**專案設定** 對話方塊。 藉由使用此對話方塊中，您可以設定 SSMA 如何將轉換函式和全域變數。 如需詳細資訊，請參閱[專案設定 &#40;轉換 &#41;&#40;SybaseToSQL &#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md).  
  
## <a name="converting-ase-database-objects"></a>轉換 ASE 資料庫物件  
若要將 ASE 資料庫物件，您先選取您要轉換的物件，然後 SSMA 執行轉換。 若要進行轉換時，檢視輸出訊息上**檢視**功能表上，選取**輸出**。  
  
**若要將 ASE 物件轉換成 SQL Server 或 SQL Azure 的語法**  
  
1.  在 Sybase 中繼資料總管，展開 ASE 伺服器，然後再展開**資料庫**。  
  
2.  選取要轉換的物件：  
  
    -   若要轉換的所有資料庫，選取核取方塊旁的 **資料庫**。  
  
    -   若要轉換或省略資料庫，選取或清除資料庫名稱旁邊的核取方塊。  
  
    -   若要轉換或省略個別結構描述，展開資料庫，展開 **結構描述**，然後選取或清除結構描述旁邊的核取方塊。  
  
    -   轉換或省略物件的類別，結構描述中，依序展開，然後選取或清除類別旁的核取方塊。  
  
    -   轉換或省略個別物件，展開類別目錄資料夾，然後選取或清除物件旁的核取方塊。  
  
3.  若要將所有選取的物件，以滑鼠右鍵按一下**資料庫**選取**轉換結構描述**。  
  
    您也可以轉換個別物件或類別目錄的物件，以滑鼠右鍵按一下物件或其包含的資料夾，然後選取**轉換結構描述**。  
  
> [!NOTE]  
> 某些 Sybase 系統函式不完全相符對等的 SQL Server 系統函數的行為。 為了模擬 Sybase ASE 行為，SSMA 會在呼叫 's2ss' 的結構描述已轉換的 SQL Server 資料庫中產生使用者定義函式。 根據專案設定，某些 SQL Server 系統函數會取代這些模擬函式。 SSMA 會建立下列使用者定義函數：  
  
||||  
|-|-|-|  
|**char_length_nvarchar**|**index_colorder**|**ssma_datepart**|  
|**char_length_varchar**|**inttohex**|**substring_nvarchar**|  
|**charindex_nvarchar**|**ssma_datediff**|**substring_varbinary**|  
|**charindex_varchar**|**hextoint**|**substring_varchar**|  
|**ulowsurr**|**to_unichar**|**ssma_current_time**|  
|**uhighsurr**|||  
  
## <a name="objects-not-supported-in-sql-azure"></a>不支援 SQL Azure 中的物件  
下列 T-SQL 關鍵字所使用 SSMA for Sybase 轉換成一般的 SQL Server 時，但不是支援這些關鍵字的 SQL Azure T-SQL 語法：  
  
||||  
|-|-|-|  
|CHECKPOINT|CREATE/ALTER/DROP DEFAULT|CREATE/DROP RULE|  
|DBCC TRACEOFF|DBCC TRACEON|授與/撤銷/拒絕全部|  
|KILL|READTEXT|SELECT INTO|  
|SET OFFSETS|SETUSER|SHUTDOWN|  
|WRITETEXT|||  
  
## <a name="viewing-conversion-problems"></a>檢視轉換問題  
某些 ASE 物件可能不會轉換。 您可以檢視摘要轉換報表來判斷轉換成功率。  
  
**若要檢視摘要報表**  
  
1.  Sybase 中繼資料總管，在選取**資料庫**。  
  
2.  在右窗格中，選取**報表** 索引標籤。  
  
    此報告會顯示摘要評估報表中的所有資料庫物件評估或轉換。 您也可以檢視個別物件的摘要報告：  
  
    -   若要檢視報表中的個別資料庫，請在 Sybase 中繼資料總管 選取的資料庫。  
  
    -   若要檢視個別的資料庫物件的報表，請在 Sybase 中繼資料總管 選取的物件。 已轉換問題的物件具有紅色錯誤圖示。  
  
無法轉換的物件，您可以檢視導致轉換失敗的語法。  
  
**若要檢視個別轉換問題**  
  
1.  在 Sybase 中繼資料總管，依序展開**資料庫**。  
  
2.  展開會顯示紅色錯誤圖示的資料庫。  
  
3.  展開**結構描述**資料夾，然後展開 結構描述會顯示紅色錯誤圖示。  
  
4.  在結構描述中，展開一個資料夾具有紅色錯誤圖示。  
  
5.  選取具有紅色錯誤圖示的物件。  
  
6.  在右窗格中，按一下 [**報表**] 索引標籤。  
  
7.  在頂端**報表** 索引標籤是下拉式清單。 如果此清單會顯示**統計資料**，變更選取範圍到**來源**。  
  
    SSMA 會顯示與原始程式碼和數個程式碼正上方的按鈕。  
  
8.  按一下**下一個問題** 按鈕。 這是指向右側的箭號以紅色錯誤圖示。  
  
    SSMA for ASE 會反白顯示在目前的物件中找到的第一個有問題的原始碼。  
  
針對無法轉換每個項目，您必須決定您想要使用該物件：  
  
-   您可以在編輯程序和觸發程序的原始程式碼**SQL**  索引標籤。  
  
-   您可以改變 ASE 物件以移除或修改程式碼有問題。 若要更新的程式碼載入 SSMA，您必須更新的中繼資料。 如需詳細資訊，請參閱[連接到 Sybase ASE &#40;SybaseToSQL &#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
-   您可以從移轉排除的物件。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中繼資料總管和 Sybase 中繼資料總管，清除項目旁邊的核取方塊，然後再載入物件到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 和 ASE 從移轉資料。  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是[載入轉換的資料庫物件至 SQL Server / SQL Azure (SybaseToSQL)](http://msdn.microsoft.com/en-us/4c59256f-99a8-4351-9559-a455813dbd06)。  
  
## <a name="see-also"></a>另請參閱  
[Sybase ASE 將資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

