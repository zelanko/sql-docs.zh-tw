---
title: 使用 SSMA Projects (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 11091d95-c488-48c3-891a-743cac94ac93
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: c9bc3f8f81d8701a584a1f4d6caee1b442746b76
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934488"
---
# <a name="working-with-ssma-projects-sybasetosql"></a>使用 SSMA 專案 (SybaseToSQL)
若要將 Sybase 彈性伺服器企業 (ASE) 資料庫移轉到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure，您必須先建立 SSMA 專案。 專案是一個檔案，其中包含您想要遷移到或 SQL Azure 之 ASE 資料庫的相關中繼資料 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將接收已遷移物件和資料之目標實例或 sql azure 的相關中繼資料， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 sql azure 連接資訊和專案設定。  
  
當您開啟專案時，它會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 中斷連接。 這可讓您離線工作。 您可以重新連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure。 如需詳細資訊，請參閱[連接到 SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)  /  [連接到 Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)。  
  
## <a name="reviewing-default-project-settings"></a>查看預設專案設定  
SSMA 包含數個選項，可用於轉換和載入資料庫物件、遷移資料，以及使用 ASE 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 同步處理 SSMA。 這些選項的預設設定適用于許多使用者。 不過，在建立新的 SSMA 專案之前，您應該先檢查選項，並視需要變更將用於所有新專案的預設值。  
  
**若要查看預設專案設定**  
  
1.  在 [**工具**] 功能表上，選取 [**預設專案設定**]。  
  
2.  在 [**遷移目標版本**] 下拉式選中選取要查看或變更其設定的專案類型，然後按一下 **[一般**] 索引標籤。  
  
3.  在左窗格中，按一下 [**轉換**]。  
  
4.  在右窗格中，檢查選項，視需要變更選項。 如需這些選項的詳細資訊，請參閱[&#40;轉換&#41; &#40;SybaseToSQL&#41;的專案設定](../../ssma/sybase/project-settings-conversion-sybasetosql.md)。  
  
5.  針對 [遷移]、[SQL Azure]、[載入物件]、[GUI] 和 [類型對應] 頁面重複步驟1-3。  
  
    -   如需有關遷移選項的詳細資訊，請參閱[&#40;遷移&#41; &#40;SybaseToSQL&#41;的專案設定](../../ssma/sybase/project-settings-migration-sybasetosql.md)。  
  
    -   如需將物件載入至之選項的詳細資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請參閱[&#40;同步處理&#41; &#40;SybaseToSQL&#41;的專案設定](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)。  
  
    -   如需 GUI 選項的詳細資訊，請參閱[&#40;gui&#41; &#40;SybaseToSQL&#41;的專案設定](../../ssma/sybase/project-settings-gui-sybasetosql.md)。  
  
    -   如需資料類型對應設定的詳細資訊，請按一下 [[專案設定] &#40;類型對應&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)。  
  
    -   如需 SQL Azure 選項的詳細資訊，請參閱[專案設定 &#40;Azure SQL Database &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)。  
  
    > [!NOTE]  
    > 只有當您在建立專案時選取 [**遷移至 SQL azure** ] 時，才會顯示 SQL azure 設定。  
  
## <a name="creating-new-projects"></a>建立新專案  
若要將資料從 ASE 資料庫移轉到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure，您必須先建立專案。  
  
**若要建立專案**  
  
1.  在 [檔案]**** 功能表上，選取 [新增專案]****。  
  
    [新增專案]  對話方塊隨即出現。  
  
2.  在 [**名稱**] 方塊中，輸入專案的名稱。  
  
3.  在 [**位置**] 方塊中，輸入或選取專案的資料夾。  
  
4.  在 [**遷移至**] 下拉式選，選取用於遷移的目標版本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 可用的選項如下︰  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Azure SQL Database  
  
然後按一下 **[確定]**。  
  
## <a name="customizing-project-settings"></a>自訂專案設定  
除了定義套用至所有新 SSMA 專案的預設專案設定之外，您還可以自訂每個專案的設定。 如需詳細資訊，請參閱[&#40;SybaseToSQL&#41;設定專案選項](../../ssma/sybase/setting-project-options-sybasetosql.md)。  
  
當您自訂來源與目標資料庫之間的資料類型對應時，您可以在專案、資料庫或物件層級定義對應。 如需型別對應的詳細資訊，請參閱將[SYBASE ASE 和 SQL Server 資料類型對應 &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)。  
  
## <a name="saving-projects"></a>儲存專案  
當您儲存專案時，SSMA 會將專案設定和選擇性的資料庫中繼資料保留到專案檔中。  
  
**儲存專案**  
  
-   **在 [檔案**] 功能表上，選取 [**儲存專案**]。  
  
    如果專案內的資料庫已變更或尚未轉換，SSMA 會提示您將中繼資料儲存到專案中。 儲存中繼資料可讓您離線工作，並將完整的專案檔案傳送給其他人，包括技術支援人員。 如果系統提示您儲存中繼資料，請執行下列動作：  
  
    1.  針對顯示 [**中繼資料遺失**] 狀態的每個資料庫，選取資料庫名稱旁邊的核取方塊。  
  
        儲存中繼資料可能需要幾分鐘的時間。 如果您不想在此時儲存中繼資料，請不要選取任何核取方塊。  
  
    2.  按一下 [儲存]  按鈕。  
  
        SSMA 會剖析 Sybase ASE 架構，並將中繼資料儲存至專案檔。  
  
## <a name="opening-projects"></a>開啟專案  
當您開啟專案時，它會從 ASE 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 中斷連接。 這可讓您離線工作。 若要更新中繼資料，請將資料庫物件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure。 若要遷移資料，您必須重新連線到 ASE 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure。  
  
**開啟專案**  
  
1.  您可以使用下列其中一個程序：  
  
    -   在 [檔案 **] 功能表上，指向 [** **最近使用的專案**]，然後選取您要開啟的專案。  
  
    -   在 [**檔案**] 功能表上，選取 [**開啟專案**]，找出 s2ssproj 專案檔案，選取檔案，然後按一下 [**開啟**]。  
  
2.  若要重新連線到 ASE，請**在 [檔案**] 功能表上，選取 [重新連線**到 Sybase**]。  
  
3.  若要重新連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure， **File**請在 [檔案] 功能表上選取 [重新連線]， **SQL Server**  /  **重新連接到 SQL Azure**。  
  
## <a name="next-step"></a>後續步驟  
遷移程式的下一個步驟是[連接到 SYBASE ASE](connecting-to-sybase-ase-sybasetosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[將 Sybase ASE 資料庫移轉至 SQL Server Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[連接到 Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)  
[連接到 SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)  
[連接到 Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
