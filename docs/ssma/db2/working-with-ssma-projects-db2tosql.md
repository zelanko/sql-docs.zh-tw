---
description: '使用 SSMA Projects (DB2ToSQL) '
title: 使用 SSMA Projects (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 07abef8a-28e8-4a66-927c-c9a5b8c938ef
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: f56387f8081ce14c68d355327c2829bf6e33c8cc
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869476"
---
# <a name="working-with-ssma-projects-db2tosql"></a>使用 SSMA Projects (DB2ToSQL) 
若要將 DB2 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您必須先建立 SSMA 專案。 專案是包含下列資訊的檔案：  
  
-   您要遷移到之 DB2 資料庫的相關中繼資料 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]將會接收已遷移物件和資料之目標實例的相關中繼資料。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接資訊。  
  
-   專案設定。  
  
當您開啟專案時，它會與 DB2 和進行中斷連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 這可讓您離線工作。 如需重新連接的相關資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請參閱 [連接到 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2tosql.md)。  
  
## <a name="reviewing-default-project-settings"></a>查看預設專案設定  
SSMA 包含數個設定，可用於轉換和載入資料庫物件、遷移資料，以及同步處理 SSMA 與 DB2 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 預設設定適用于許多使用者。 不過，在建立新的 SSMA 專案之前，您應該先檢查設定。 如果您想要的話，可以變更將用於所有新專案的預設設定。  
  
**若要檢查預設專案設定**  
  
1.  按一下 [ **工具** ] 功能表上的 [ **預設專案設定**]。  
  
2.  在 [ **遷移目標版本** ] 下拉式清單中，選取需要查看或變更設定的專案類型，然後按一下 **[一般** ] 索引標籤。  
  
3.  在左窗格中，按一下 [ **轉換**]。  
  
4.  在右窗格中，檢查並視需要變更設定。 如需這些設定的詳細資訊，請參閱 [&#40;轉換&#41; &#40;DB2ToSQL&#41;的專案設定 ](../../ssma/db2/project-settings-conversion-db2tosql.md)。  
  
5.  針對遷移、同步處理、載入系統物件、GUI 和類型對應頁面重複步驟1-3。  
  
    -   如需有關遷移設定的詳細資訊，請參閱 [&#40;遷移&#41; &#40;DB2ToSQL&#41;的專案設定 ](../../ssma/db2/project-settings-migration-db2tosql.md)。  
  
    -   如需系統物件設定的詳細資訊，請參閱 [&#40;載入系統物件&#41; &#40;DB2ToSQL&#41;的專案設定 ](../../ssma/db2/project-settings-loading-system-objects-db2tosql.md)。  
  
    -   如需同步處理設定的詳細資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請參閱 [&#40;同步處理的專案設定&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md)。  
  
    -   如需 GUI 設定的詳細資訊，請參閱 [&#40;gui 的專案設定&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-gui-db2tosql.md)。  
  
    -   如需資料類型對應設定的詳細資訊，請參閱 [&#40;類型對應的專案設定&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md)。  
  
## <a name="creating-new-projects"></a>建立新專案  
若要將資料從 DB2 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您必須先建立專案。  
  
**若要建立專案**  
  
1.  按一下 [檔案] 功能表上的 [新增專案]。  
  
    [新增專案]  對話方塊隨即出現。  
  
2.  在 [ **名稱** ] 方塊中，輸入專案的名稱。  
  
3.  在 [ **位置** ] 方塊中，輸入或選取專案的資料夾，然後按一下 **[確定]**。  
  
4.  在 [ **遷移至** ] 下拉式清單中，選取要用於遷移的目標版本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 可用的選項如下︰  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Azure SQL Database  
  
## <a name="customizing-project-settings"></a>自訂專案設定  
除了定義適用于所有新 SSMA 專案的預設專案設定以外，您還可以自訂每個專案的設定。 如需詳細資訊，請參閱 [設定專案選項 &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md) 和相關章節。  
  
當您自訂來源與目標資料庫之間的資料類型對應時，可以在專案、資料庫或物件層級定義對應。 如需詳細資訊，請參閱將 [DB2 和 SQL Server 資料類型對應 &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)。  
  
## <a name="saving-projects"></a>儲存專案  
當您儲存專案時，SSMA 會將專案設定（並選擇性地將資料庫中繼資料）保留至專案檔。  
  
**儲存專案**  
  
-   **在 [檔案**] 功能表上，按一下 [**儲存專案**]。  
  
    如果專案中的架構已變更或尚未轉換，SSMA 會提示您載入並儲存中繼資料。 載入和儲存中繼資料可讓您離線工作。 它也可讓您將完整的專案檔傳送給其他人，例如技術支援人員。 如果系統提示您儲存中繼資料，請執行下列動作：  
  
    1.  針對顯示 **遺漏中繼資料** 狀態的每個架構，選取資料庫名稱旁邊的核取方塊。  
  
        儲存中繼資料可能需要幾分鐘的時間。 如果您還沒有想要儲存中繼資料，請勿選取任何核取方塊。  
  
    2.  按一下 [儲存]  按鈕。  
  
        SSMA 會剖析 DB2 架構，並將中繼資料儲存至專案檔。  
  
## <a name="opening-projects"></a>開啟專案  
當您開啟專案時，它會與 DB2 和之間的中斷連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 這可讓您離線工作。 若要更新中繼資料，請將資料庫物件載入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 若要遷移資料，您必須重新連接到 DB2 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
**開啟專案**  
  
1.  您可以使用下列其中一個程序：  
  
    -   在 [檔案 **] 功能表上，指向 [** **最近使用的專案**]，然後按一下您要開啟的專案。  
  
    -   在 [ **檔案** ] 功能表上，選取 [ **開啟專案**]，找出 o2ssproj 專案檔，選取檔案，然後按一下 [ **開啟**]。  
  
2.  若要重新連接到 DB2，請 **在 [檔案** ] 功能表上，按一下 [ **重新連接到 db2**]。  
  
3.  若要重新連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請 **File** 在 [檔案] 功能表上，按一下 [**重新連接] 以 SQL Server**。  
  
## <a name="next-step"></a>後續步驟  
遷移程式的下一個步驟是 [連接到 DB2 資料庫](./connecting-to-db2-database-db2tosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[將 DB2 資料庫移轉至 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
[連接到 DB2 資料庫 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)  
[連接至 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2tosql.md)  
