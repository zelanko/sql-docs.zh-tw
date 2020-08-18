---
description: 使用 SSMA 專案 (MySQLToSQL)
title: 使用 SSMA Projects (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Working with SSMA projects, create new project
- Working with SSMA projects, customize settings
- Working with SSMA projects, Open project
- Working with SSMA projects, Save project
ms.assetid: 9e4394e9-f177-41d9-839e-5d53a9c9b840
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: d6a1bbc7b47531c66e27818e8673a7c6aa9723c8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492413"
---
# <a name="working-with-ssma-projects-mysqltosql"></a>使用 SSMA 專案 (MySQLToSQL)
若要將 MySQL 資料庫遷移至 SQL Server 或 SQL Azure，您必須先建立 SSMA 專案。 專案是包含下列資訊的檔案：  
  
-   您要遷移至 SQL Server 或 SQL Azure 之 MySQL 資料庫的相關中繼資料。  
  
-   將會接收已遷移物件和資料之 SQL Server 或 SQL Azure 目標實例的相關中繼資料。  
  
-   SQL Server 或 SQL Azure 連接資訊。  
  
-   專案設定。  
  
當您開啟專案時，它會與 MySQL 和 SQL Server 或 SQL Azure 中斷連線。 這可讓您離線工作。 如需有關重新連接到 SQL Server 的詳細資訊，請參閱 [連接至 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="reviewing-default-project-settings"></a>查看預設專案設定  
SSMA 包含數個設定，可用於轉換和載入資料庫、遷移資料，以及將 SSMA 與 MySQL 和 SQL Server 或 SQL Azure 進行同步處理。 預設設定適用于許多使用者。 不過，在建立新的 SSMA 專案之前，您應該先檢查設定。 如有需要，您可以變更將用於所有新專案的預設設定。  
  
##### <a name="to-review-default-project-settings"></a>若要檢查預設專案設定  
  
1.  從 [**工具**] 功能表選取 [**預設專案設定**]。  
  
2.  在 [ **遷移目標版本** ] 下拉式清單中選取要查看/變更設定的專案類型，然後按一下 **[一般** ] 索引標籤。  
  
3.  在左窗格中，按一下 [ **轉換**]。  
  
4.  在右窗格中，檢查並視需要變更設定。 如需這些設定的詳細資訊，請參閱 [&#40;轉換&#41; &#40;MySQLToSQL&#41;的專案設定 ](../../ssma/mysql/project-settings-conversion-mysqltosql.md) 。  
  
5.  針對 [遷移]、[同步處理]、[SQL Azure]、[GUI] 和 [類型對應] 頁面重複步驟1-3。  
  
-   如需有關遷移設定的詳細資訊，請參閱 [&#40;遷移&#41; &#40;MySQLToSQL&#41;的專案設定 ](../../ssma/mysql/project-settings-migration-mysqltosql.md)。  
  
-   如需同步處理至 SQL Server 之設定的相關資訊，請參閱 [&#40;同步處理&#41; &#40;MySQLToSQL&#41;的專案設定 ](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)。  
  
-   如需 GUI 設定的詳細資訊，請參閱 [ (gui 的專案設定)  (SSMA 一般) ](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)。  
  
-   如需資料類型對應設定的詳細資訊，請參閱 [&#40;類型對應的專案設定&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)。  
  
-   如需有關 SQL Azure 設定的詳細資訊，請參閱 [&#40;Azure SQL Database&#41; &#40;MySQLToSQL&#41;的專案設定 ](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)。  
  
> [!NOTE]  
> 只有當您在建立專案時選取 [ **遷移至 SQL azure** ] 時，才會顯示 sql azure 設定。  
  
## <a name="creating-new-projects"></a>建立新專案  
若要將資料從 MySQL 資料庫遷移至 SQL Server 或 SQL Azure，您必須建立專案。  
  
##### <a name="to-create-a-new-project"></a>建立新的專案  
  
1.  從 **[檔案**] 功能表選取 [**新增專案**]。 [新增專案]  對話方塊隨即出現。 在 [檔案]**** 功能表上，選取 [新增專案]****。 [新增專案]  對話方塊隨即出現。  
  
2.  在 [ **名稱** ] 方塊中，輸入專案的名稱。  
  
3.  在 [ **位置** ] 方塊中，輸入或選取專案的資料夾。  
  
4.  在 [ **遷移至** ] 下拉式清單中，選取要用於遷移的目標版本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 可用的選項如下︰  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   Azure SQL Database  
  
然後按一下 **[確定]**  
  
SSMA 會建立專案檔。  
  
## <a name="customizing-project-settings"></a>自訂專案設定  
除了定義適用于所有新 SSMA 專案的預設專案設定以外，您也可以自訂每個專案的設定。 如需詳細資訊，請參閱 [設定專案選項 &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)。  
  
當您自訂來源與目標資料庫之間的資料類型對應時，可以在專案、資料庫或物件層級定義對應。 如需詳細資訊，請參閱將 [MySQL 和 SQL Server 資料類型對應 &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)。  
  
## <a name="saving-projects"></a>儲存專案  
[儲存專案] 功能可讓使用者基本上儲存專案設定，並選擇性地將資料庫中繼資料儲存至 SSMA 專案檔案。  
  
##### <a name="to-save-a-project"></a>儲存專案  
  
-   **在 [檔案**] 功能表上，選取 [**儲存**專案]。  
  
如果專案內的資料庫變更或尚未轉換，SSMA 會提示您載入並儲存中繼資料。 載入和儲存中繼資料可讓您離線工作。 它也可讓您將完整的專案檔傳送給其他人，例如技術支援人員。 如果系統提示您儲存中繼資料，請執行下列動作：  
  
1.  針對顯示 **遺漏中繼資料**狀態的每個資料庫，選取資料庫名稱旁邊的核取方塊。 儲存中繼資料可能需要幾分鐘的時間。 如果您不想在此時儲存中繼資料，請不要選取任何核取方塊。  
  
2.  按一下 [檔案] 。  
  
SSMA 會剖析 MySQL 架構，並將中繼資料儲存至專案檔。  
  
## <a name="opening-projects"></a>開啟專案  
當您開啟專案時，它會與 MySQL 和 SQL Server 或 SQL Azure 中斷連線。 這可讓您離線工作。 若要更新中繼資料，請將資料庫物件載入 SQL Server 或 SQL Azure。 若要遷移資料，您必須重新連接到 SQL Server 或 SQL Azure。  
  
##### <a name="to-open-a-project"></a>開啟專案  
  
1.  您可以使用下列其中一個程序：  
  
    1.  **在 [檔案**] 功能表上，指向 [**最近使用的專案**]。  
  
    2.  選取您要開啟的專案。  
  
    3.  在 [ **檔案** ] 功能表上，選取 [ **開啟專案**]，找出 m2ssproj 專案檔，選取檔案，然後按一下 [ **開啟**]。  
  
2.  若要重新連線至 MySQL，請 **在 [檔案** ] 功能表上選取 [重新連線 **至 mysql**]。  
  
3.  若要重新連線到 SQL Server，請 **在 [檔案** ] 功能表上選取 [ **重新連接到 SQL Server**。  
  
4.  若要重新連線到 SQL Azure，請 **在 [檔案** ] 功能表上選取 [ **重新連接到 sql azure]。**  
  
## <a name="next-step"></a>後續步驟  
遷移程式的下一個步驟是 [連接到 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
## <a name="see-also"></a>另請參閱  
[連接至 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
[將 MySQL 資料庫遷移至 SQL Server Azure SQL Database &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[連接至 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
[連接至 Azure SQL Database &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
