---
title: 轉換 Sybase ASE 資料庫物件 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Converting Database Objects
ms.assetid: 509cb65d-2f54-427a-83d7-37919cc4e3e3
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 86adf372dfd590f0cac1d8ac872501fb12ab1e7b
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38980660"
---
# <a name="converting-sap-ase-database-objects-sybasetosql"></a>轉換的 SAP ASE 資料庫物件 (SybaseToSQL)
您已經連接到 SAP Adaptive Server Enterprise (ASE) 之後，連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 和設定專案和對應的資料選項，您可以將轉換至 SAP Adaptive Server Enterprise (ASE) 資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL database物件。  
  
## <a name="the-conversion-process"></a>轉換程序  
轉換的資料庫物件從 ASE 中取得的物件定義、 將它們轉換成類似[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 物件，並接著將這項資訊載入至 SSMA 中繼資料。 它不會載入到執行個體資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL。 您接著可以檢視的物件和其屬性，使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 中繼資料總管。
  
在轉換期間 SSMA 輸出將訊息列印至輸出窗格和錯誤訊息，以**錯誤清單**窗格。 使用輸出和錯誤的資訊來判斷是否需要修改您的 ASE 資料庫或您的轉換程序，以便取得所需的轉換結果。  
  
## <a name="setting-conversion-options"></a>設定轉換選項  
在轉換前的物件，檢閱中的專案轉換選項**專案設定** 對話方塊。 藉由使用這個對話方塊中，您可以設定 SSMA 如何將轉換函式和全域變數。 如需詳細資訊，請參閱 <<c0> [ 專案設定&#40;轉換&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)。</c0>  
  
## <a name="converting-ase-database-objects"></a>轉換 ASE 資料庫物件  
若要將 ASE 資料庫物件的轉換，先選取您想要轉換的物件，就會執行轉換的 SSMA。 若要檢視轉換期間的輸出訊息上**檢視**功能表上，選取**輸出**。  
  
**若要將 ASE 物件轉換成 SQL Server 或 SQL Azure 的語法**  
  
1.  在 Sybase 中繼資料總管 中，展開 ASE 伺服器，然後展開**資料庫**。  
  
2.  選取要轉換的物件：  
  
    -   若要將所有的資料庫轉換，選取核取方塊旁**資料庫**。  
  
    -   若要轉換，或略過資料庫，選取或清除資料庫名稱旁邊的核取方塊。  
  
    -   若要轉換，或省略的個別結構描述，展開資料庫，依序展開**結構描述**，然後選取或清除結構描述旁邊的核取方塊。  
  
    -   若要轉換，或略過的物件類別，展開結構描述，然後選取或清除類別旁的核取方塊。  
  
    -   轉換或省略個別物件，依序展開 [分類] 資料夾中，然後選取或清除物件旁的核取方塊。  
  
3.  若要將所有選取的物件，以滑鼠右鍵按一下**資料庫**，然後選取**轉換的結構描述**。  
  
    您也可以轉換個別物件或類別目錄的物件，以滑鼠右鍵按一下 物件或其包含的資料夾，然後選取**轉換的結構描述**。  
  
> [!NOTE]  
> 部分的 SAP ASE 系統函式不完全比對等的 SQL Server 系統函式的行為。 若要模擬的 SAP ASE 行為，SSMA 會產生使用者定義函式在呼叫 's2ss' 的結構描述已轉換的 SQL Server 資料庫中。 根據專案設定中，有些 SQL Server 系統函數會取代這些模擬函式。 SSMA 會建立下列使用者定義函式：  
  
||||  
|-|-|-|  
|**char_length_nvarchar**|**index_colorder**|**ssma_datepart**|  
|**char_length_varchar**|**inttohex**|**substring_nvarchar**|  
|**charindex_nvarchar**|**ssma_datediff**|**substring_varbinary**|  
|**charindex_varchar**|**hextoint**|**substring_varchar**|  
|**ulowsurr**|**to_unichar**|**ssma_current_time**|  
|**uhighsurr**|||  
  
## <a name="objects-not-supported-in-azure-sql"></a>不支援在 SQL Azure 中的物件  
以下的 T-SQL 關鍵字會使用 SSMA 適用於 SAP ASE 期間轉換為 SQL Server 內部部署，但是 SQL Azure T-SQL 語法不支援這些關鍵字：  
  
||||  
|-|-|-|  
|CHECKPOINT|CREATE/ALTER/DROP DEFAULT|CREATE/DROP RULE|  
|DBCC TRACEOFF|DBCC TRACEON|GRANT/REVOKE/DENY ALL|  
|KILL|READTEXT|SELECT INTO|  
|SET OFFSETS|SETUSER|SHUTDOWN|  
|WRITETEXT|||  
  
## <a name="viewing-conversion-problems"></a>檢視轉換的問題  
SAP ASE 的某些物件可能不會轉換。 您可以檢視摘要轉換報告，以判斷轉換成功比率。  
  
**若要檢視摘要報表**  
  
1.  在 Sybase 中繼資料總管 中，選取**資料庫**。  
  
2.  在右窗格中，選取**報表** 索引標籤。  
  
    此報告會顯示所有的資料庫物件尚未評估或轉換的摘要的評定報告。 您也可以檢視個別物件的摘要報告：  
  
    -   若要檢視個別資料庫的報表，請在 Sybase 中繼資料總管 中選取的資料庫。  
  
    -   若要檢視個別的資料庫物件的報表，請在 Sybase 中繼資料總管 中選取的物件。 有轉換問題的物件具有紅色錯誤圖示。  
  
針對無法轉換的物件，您可以檢視導致轉換失敗的語法。  
  
**若要檢視個別轉換的問題**  
  
1.  在 Sybase 中繼資料總管 中，依序展開**資料庫**。  
  
2.  展開會顯示紅色錯誤圖示的資料庫。  
  
3.  依序展開**結構描述**資料夾，然後展開 結構描述會顯示紅色錯誤圖示。  
  
4.  在結構描述中，展開一個資料夾具有紅色錯誤圖示。  
  
5.  選取具有紅色錯誤圖示的物件。  
  
6.  在右窗格中，選取**報表** 索引標籤。  
  
7.  在頂端**報表** 索引標籤上是下拉式清單。 如果此清單會顯示**統計資料**，變更選取範圍往**來源**。  
  
    SSMA 會顯示在原始程式碼和數個按鈕正上方的程式碼。  
  
8.  選取 **下一個問題**，紅色錯誤圖示，向右箭號。  
  
    適用於 SAP ASE 的 SSMA 會反白顯示在目前的物件中找到的第一個有問題的來源程式碼。  
  
每個項目無法轉換，您必須決定您想要與該物件：  
  
-   您可以在編輯程序和觸發程序的原始程式碼**SQL**  索引標籤。  
  
-   您可以改變的 SAP ASE 物件，以移除或修改有問題的程式碼。 若要更新的程式碼載入 SSMA 中，您必須更新的中繼資料。 如需詳細資訊，請參閱 <<c0> [ 連接到 SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)。</c0>  
  
-   您可以從移轉排除的物件。 在 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 中繼資料總管和 Sybase 中繼資料總管] 中，清除項目旁的核取方塊，然後再載入到物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 和 SAP ase 資料移轉。  
  
## <a name="next-steps"></a>後續的步驟  
移轉程序的下一個步驟是[載入轉換的資料庫物件載入 SQL Server / SQL Azure (SybaseToSQL)](http://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06)。  
  
## <a name="see-also"></a>另請參閱  
[SAP ASE 資料庫移轉至 SQL Server-Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
