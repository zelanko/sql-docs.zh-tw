---
title: 使用 SSMA 專案 (SybaseToSQL) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 11091d95-c488-48c3-891a-743cac94ac93
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7e1be086b891d6888c6509b15adc6664b3022978
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47830126"
---
# <a name="working-with-ssma-projects-sybasetosql"></a>使用 SSMA 專案 (SybaseToSQL)
若要移轉 Sybase 調整伺服器企業 (ASE) 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 您先建立 SSMA 專案。 專案是一個包含您想要遷移到 ASE 資料庫相關的中繼資料檔案[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，目標執行個體的相關中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或遷移的物件和資料，會收到的 SQL Azure[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure連線資訊和專案設定。  
  
當您開啟專案時，它會中斷連線從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 這可讓您離線工作。 您可以重新連線到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 如需詳細資訊，請參閱[連線到 SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md) / [Azure SQL 資料庫連線&#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)。  
  
## <a name="reviewing-default-project-settings"></a>檢閱預設的專案設定  
SSMA 包含數個選項，藉以轉換和載入資料庫物件，移轉資料，並與 ASE 中同步處理 SSMA 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 這些選項的預設設定可適用於許多使用者項目。 不過，您建立新的 SSMA 專案之前，您應該檢閱的選項，如果您想要變更將會用於所有新專案的預設值。  
  
**若要檢視預設的專案設定**  
  
1.  在 **工具**功能表上，選取**預設專案設定**。  
  
2.  選取專案類型，在**遷移目標版本**可才能檢視或變更哪些設定，然後按一下向下的距離**一般** 索引標籤。  
  
3.  在左窗格中，按一下 **轉換**。  
  
4.  在右窗格中，檢閱的選項，變更所需的選項。 如需有關這些選項的詳細資訊，請參閱[專案設定&#40;轉換&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)。  
  
5.  重複步驟 1-3 的移轉、 SQL Azure、 載入的物件、 GUI，和型別對應的頁面。  
  
    -   移轉選項的相關資訊，請參閱[專案設定&#40;遷移&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md)。  
  
    -   如需載入物件到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱[專案設定&#40;同步處理&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)。  
  
    -   如需有關 GUI 選項的詳細資訊，請參閱[專案設定&#40;GUI&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md)。  
  
    -   如需有關資料型別對應設定的詳細資訊，請按一下[專案設定&#40;型別對應&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)。  
  
    -   如需有關 SQL Azure 選項的詳細資訊，請參閱[專案設定&#40;Azure SQL DB &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)。  
  
    > [!NOTE]  
    > 只有在您選取時，會顯示 SQL Azure 設定**移轉至 SQL Azure**建立的專案。  
  
## <a name="creating-new-projects"></a>建立新專案  
若要從 ASE 資料庫遷移資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure，您必須先建立專案。  
  
**若要建立專案**  
  
1.  在 [檔案] 功能表上，選取 [新增專案]。  
  
    [新增專案]  對話方塊隨即出現。  
  
2.  在 **名稱**方塊中，輸入您專案的名稱。  
  
3.  在**位置**方塊中，輸入或選取專案的資料夾。  
  
4.  在**遷移至**下拉式清單，請選取目標版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]遷移所使用的。 可用的選項如下：  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Azure 的 SQL 資料庫  
  
然後按一下 **確定**。  
  
## <a name="customizing-project-settings"></a>自訂專案設定  
除了定義套用到所有新的 SSMA 專案的預設專案設定，您可以自訂每個專案的設定。 如需詳細資訊，請參閱[設定專案選項&#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)。  
  
當您自訂來源和目標資料庫之間的資料型別對應時，您可以定義在專案、 資料庫或物件層級的對應。 如需有關型別對應的詳細資訊，請參閱[對應 Sybase ASE 和 SQL Server 資料型別&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)。  
  
## <a name="saving-projects"></a>儲存專案  
當您儲存專案時，專案設定，並選擇性地資料庫中繼資料中的，專案檔，也將會保留 SSMA。  
  
**若要儲存專案**  
  
-   在**檔案**功能表上，選取**儲存專案**。  
  
    如果資料庫專案內已變更，或尚未轉換，SSMA 會提示您儲存到專案的中繼資料。 儲存中繼資料，將可讓您離線工作，並將完成的專案檔案傳送給其他人，包括技術支援人員。 如果系統提示您儲存中繼資料，請執行下列動作：  
  
    1.  每個資料庫，會顯示狀態**中繼資料遺漏**，選取資料庫名稱旁邊的核取方塊。  
  
        儲存中繼資料，可能需要幾分鐘的時間。 如果您不想在此時儲存中繼資料，請勿選取任何核取方塊。  
  
    2.  按一下 [**儲存**] 按鈕。  
  
        SSMA 會剖析 Sybase ASE 結構描述，並將中繼資料儲存到專案檔。  
  
## <a name="opening-projects"></a>開啟專案  
當您開啟專案時，它會中斷連線從 ASE 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 這可讓您離線工作。 若要更新中繼資料，載入資料庫物件到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。 若要移轉資料，您必須重新連線到 ASE 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure。  
  
**若要開啟專案**  
  
1.  您可以使用下列其中一個程序：  
  
    -   在**檔案** 功能表上指向**最近使用的專案**，然後選取您要開啟的專案。  
  
    -   在**檔案**功能表上，選取**開啟的專案**，找出.s2ssproj 的專案檔案、 選取 [檔案]，然後按一下**開啟**。  
  
2.  若要重新連線到 ASE 上,**檔案**功能表上，選取**重新連線到 Sybase**。  
  
3.  若要重新連線到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 上**檔案**功能表上，選取**重新連線到 SQL Server** / **重新連線到 SQL Azure**。  
  
## <a name="next-step"></a>下一個步驟  
遷移程序的下一個步驟是[連線 Sybase ASE 到](connecting-to-sybase-ase-sybasetosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[連線到 Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)  
[連線到 SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)  
[連線到 Azure 的 SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
