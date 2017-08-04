---
title: "使用 SSMA 專案 (SybaseToSQL) |Microsoft 文件"
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
ms.assetid: 11091d95-c488-48c3-891a-743cac94ac93
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 957f4148fc200fee98b29fed1f28a17bc8661d07
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="working-with-ssma-projects-sybasetosql"></a>使用 SSMA 專案 (SybaseToSQL)
若要將 Sybase Adaptive Server Enterprise (ASE) 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，您先建立 SSMA 專案。 專案是包含您想要移轉至 ASE 資料庫的相關中繼資料的檔案[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，目標執行個體的相關中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 移轉的物件和資料，將會接收[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 連接資訊，以及專案設定。  
  
當您開啟專案時，它已中斷連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 這可讓您離線工作。 您可以重新連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 如需詳細資訊，請參閱[連接到 SQL Server &#40;SybaseToSQL &#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)  / [連接到 Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md).  
  
## <a name="reviewing-default-project-settings"></a>檢閱預設的專案設定  
SSMA 包含數個選項來轉換和載入資料庫物件時，移轉資料，並與 ASE 同步 SSMA 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 這些選項的預設設定則適用於許多使用者。 不過，在建立新的 SSMA 專案之前，您應該檢閱的選項，如果您想要的變更將用於所有新專案的預設值。  
  
**若要檢閱預設的專案設定**  
  
1.  在**工具**功能表上，選取**預設專案設定**。  
  
2.  選取 [專案類型中的**移轉的目標版本**下拉式清單可檢視或變更需要哪些設定，然後按一下**一般**] 索引標籤。  
  
3.  在左窗格中，按一下 **轉換**。  
  
4.  在右窗格中，檢閱選項 變更為所需的選項。 如需有關這些選項的詳細資訊，請參閱[專案設定 &#40;轉換 &#41;&#40;SybaseToSQL &#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md).  
  
5.  重複步驟 1-3 的移轉、 SQL Azure、 載入物件，GUI，和型別對應頁面。  
  
    -   移轉選項的相關資訊，請參閱[專案設定 &#40;移轉 &#41;&#40;SybaseToSQL &#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md).  
  
    -   如需有關載入物件到選項資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，請參閱[專案設定 &#40;同步處理 &#41;&#40;SybaseToSQL &#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md).  
  
    -   如需有關 GUI 選項的詳細資訊，請參閱[專案設定 &#40;GUI &#41;&#40;SybaseToSQL &#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md).  
  
    -   如需有關資料類型對應設定的詳細資訊，請按一下[專案設定 &#40;型別對應 &#41;&#40;SybaseToSQL &#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md).  
  
    -   如需有關 SQL Azure 選項的詳細資訊，請參閱[專案設定 &#40;Azure SQL DB &#41;&#40;SybaseToSQL &#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md).  
  
    > [!NOTE]  
    > 只有當您選取時，將會顯示 SQL Azure 設定**移轉至 SQL Azure**建立專案時。  
  
## <a name="creating-new-projects"></a>建立新的專案  
若要將資料從 ASE 資料庫移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，您必須先建立專案。  
  
**若要建立專案**  
  
1.  在 [檔案] 功能表上，選取 [新增專案]。  
  
    [新增專案]  對話方塊隨即出現。  
  
2.  在**名稱**方塊中，輸入您的專案名稱。  
  
3.  在**位置**方塊中，輸入或選取專案的資料夾。  
  
4.  在**移轉至**下拉式清單中，選取的目標版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]用於移轉。 可用的選項有：  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016  
  
    -   Azure SQL DB  
  
然後按一下 **確定**。  
  
## <a name="customizing-project-settings"></a>自訂專案設定  
除了定義套用到所有新的 SSMA 專案的預設專案設定，您可以自訂每個專案的設定。 如需詳細資訊，請參閱[設定專案選項 &#40;SybaseToSQL &#41;](../../ssma/sybase/setting-project-options-sybasetosql.md).  
  
當您自訂來源和目標資料庫之間的資料類型對應時，您可以定義在專案、 資料庫或物件層級的對應。 如需型別對應的詳細資訊，請參閱[對應 Sybase ASE 和 SQL Server 資料類型 &#40;SybaseToSQL &#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
## <a name="saving-projects"></a>儲存專案  
當您儲存專案時，SSMA 會保留與專案設定，以及選擇性地資料庫中繼資料，加入專案檔。  
  
**若要儲存專案**  
  
-   在**檔案**功能表上，選取**儲存專案**。  
  
    如果在專案中的資料庫已變更或尚未轉換，SSMA 會提示您，將中繼資料儲存至專案。 儲存中繼資料可讓您離線工作並將完整的專案檔案傳送給其他人，包括技術支援人員。 如果系統提示您儲存中繼資料，請執行下列動作：  
  
    1.  每個資料庫的狀態是 **中繼資料遺漏**，選取資料庫名稱旁邊的核取方塊。  
  
        儲存中繼資料，可能需要幾分鐘的時間。 如果不想此時儲存中繼資料，請勿選取任何核取方塊。  
  
    2.  按一下 [ **儲存** ] 按鈕。  
  
        SSMA 會剖析 Sybase ASE 結構描述，並將中繼資料儲存到專案檔。  
  
## <a name="opening-projects"></a>開啟專案  
當您開啟專案時，它已中斷連接從 ASE 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 這可讓您離線工作。 若要更新的中繼資料，資料庫物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 若要移轉的資料，您必須重新連接到 ASE 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
**若要開啟專案**  
  
1.  您可以使用下列其中一個程序：  
  
    -   在**檔案**功能表上，指向**最近使用的專案**，然後選取您想要開啟專案。  
  
    -   在**檔案**功能表上，選取**開啟專案**、 尋找.s2ssproj 專案檔中，選取檔案，並按一下**開啟**。  
  
2.  若要重新連線到 ASE 上,**檔案**功能表上，選取**重新連接到 Sybase**。  
  
3.  若要重新連線到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 上**檔案**功能表上，選取**重新連接到 SQL Server** / **重新連接到 SQL Azure**。  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是[連接到 Sybase ASE](http://msdn.microsoft.com/en-us/a45a2330-9175-4c9e-af38-ef920e350614)。  
  
## <a name="see-also"></a>另請參閱  
[Sybase ASE 將資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[連接到 Sybase ASE &#40;SybaseToSQL &#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)  
[連接到 SQL Server &#40;SybaseToSQL &#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)  
[連接到 Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  

