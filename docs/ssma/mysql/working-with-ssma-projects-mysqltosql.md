---
title: 使用 SSMA 專案 (MySQLToSQL) |Microsoft 文件
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
helpviewer_keywords:
- Working with SSMA projects, create new project
- Working with SSMA projects, customize settings
- Working with SSMA projects, Open project
- Working with SSMA projects, Save project
ms.assetid: 9e4394e9-f177-41d9-839e-5d53a9c9b840
caps.latest.revision: 20
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6aee06b09e4743f678779dc93746a97c580df787
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2018
ms.locfileid: "34776744"
---
# <a name="working-with-ssma-projects-mysqltosql"></a>使用 SSMA 專案 (MySQLToSQL)
若要移轉至 SQL Server 或 SQL Azure 的 MySQL 資料庫，您必須先建立的 SSMA 專案。 專案是檔案，包含下列資訊：  
  
-   您想要移轉至 SQL Server 或 SQL Azure 的 MySQL 資料庫的相關中繼資料。  
  
-   SQL Server 或 SQL Azure 移轉的物件和資料將會接收目標執行個體的相關中繼資料。  
  
-   SQL Server 或 SQL Azure 連接資訊。  
  
-   專案設定。  
  
當您開啟專案時，它已中斷連接 MySQL 及 SQL Server 或 SQL Azure。 可讓您離線工作。 如需有關如何重新連接到 SQL Server 的詳細資訊，請參閱[連接到 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="reviewing-default-project-settings"></a>檢閱預設的專案設定  
SSMA 會包含數個設定的轉換和載入資料庫、 遷移資料及同步處理 SSMA MySQL 及 SQL Server 或 SQL Azure。 預設設定則適用於許多使用者。 不過，在建立新的 SSMA 專案之前，您應該檢閱的設定。 如有需要，您可以變更預設設定將用於所有新的專案。  
  
##### <a name="to-review-default-project-settings"></a>若要檢閱預設的專案設定  
  
1.  選取**預設專案設定**從**工具**功能表。  
  
2.  選取 [專案類型中的**移轉的目標版本**下拉式清單可檢視 / 變更哪些設定，然後按一下**一般**] 索引標籤。  
  
3.  在左窗格中，按一下 **轉換**。  
  
4.  在右窗格中，檢閱並視需要變更設定。 如需有關這些設定的詳細資訊，請參閱[專案設定&#40;轉換&#41; &#40;MySQLToSQL&#41; ](../../ssma/mysql/project-settings-conversion-mysqltosql.md) 。  
  
5.  重複步驟 1-3 的移轉、 同步處理 SQL Azure、 GUI，，和型別對應頁面。  
  
-   移轉設定的相關資訊，請參閱[專案設定&#40;移轉&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)。  
  
-   設定 SQL server 的同步處理的相關資訊，請參閱[專案設定&#40;同步&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)。  
  
-   GUI 設定的相關資訊，請參閱[專案設定 (GUI) （SSMA 常見）](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693)。  
  
-   資料類型對應設定的相關資訊，請參閱[專案設定&#40;型別對應&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)。  
  
-   設定 SQL Azure 的相關資訊，請參閱[專案設定&#40;Azure SQL DB&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)。  
  
> [!NOTE]  
> 只有當您選取時，將會顯示 SQL Azure 設定**移轉至 SQL Azure**建立專案時。  
  
## <a name="creating-new-projects"></a>建立新的專案  
若要將資料從 MySQL 資料庫移轉至 SQL Server 或 SQL Azure，您必須建立專案。  
  
##### <a name="to-create-a-new-project"></a>建立新的專案  
  
1.  選取**新專案**從**檔案**功能表。 [新增專案]  對話方塊隨即出現。 在 [檔案] 功能表上，選取 [新增專案]。 [新增專案]  對話方塊隨即出現。  
  
2.  在**名稱**方塊中，輸入您的專案名稱。  
  
3.  在**位置**方塊中，輸入或選取專案的資料夾。  
  
4.  在**移轉至**下拉式清單中，選取的目標版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]用於移轉。 可用的選項有：  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014  
  
    -   Azure SQL DB  
  
然後按一下  **確定**  
  
SSMA 會建立專案檔。  
  
## <a name="customizing-project-settings"></a>自訂專案設定  
除了定義預設值套用到所有新的 SSMA 專案的專案設定也可以自訂每個專案的設定。 如需詳細資訊，請參閱[設定專案選項&#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)。  
  
當您自訂來源和目標資料庫之間的資料類型對應時，您可以定義在專案、 資料庫或物件層級的對應。 如需詳細資訊，請參閱[對應 MySQL 及 SQL Server 資料類型&#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)。  
  
## <a name="saving-projects"></a>儲存專案  
儲存專案功能可讓使用者基本上 SSMA 專案檔中儲存的專案設定，並選擇性地資料庫中繼資料。  
  
##### <a name="to-save-a-project"></a>儲存專案  
  
-   在**檔案**功能表上，選取**儲存**專案。  
  
如果在專案中的資料庫已變更或尚未轉換，SSMA 會提示您以載入和儲存中繼資料。 載入和儲存中繼資料可讓您離線工作。 它也可讓您將完成的專案檔案傳送給其他人，例如技術支援人員。 如果系統提示您儲存中繼資料，請執行下列動作：  
  
1.  每個資料庫的狀態是 **中繼資料遺漏**，選取資料庫名稱旁邊的核取方塊。 儲存中繼資料，可能需要幾分鐘的時間。 如果不想此時儲存中繼資料，請勿選取任何核取方塊。  
  
2.  按一下 **[儲存]**。  
  
SSMA 會剖析 MySQL 結構描述，並將中繼資料儲存到專案檔。  
  
## <a name="opening-projects"></a>開啟專案  
當您開啟專案時，它已中斷連接，從 MySQL 及 SQL Server 或 SQL Azure。 這可讓您離線工作。 若要更新的中繼資料，資料庫的物件載入 SQL Server 或 SQL Azure。 若要移轉的資料，您必須重新連接到 SQL Server 或 SQL Azure。  
  
##### <a name="to-open-a-project"></a>開啟專案  
  
1.  您可以使用下列其中一個程序：  
  
    1.  在**檔案**功能表上，指向**最近使用的專案**。  
  
    2.  選取您想要開啟的專案。  
  
    3.  在**檔案**功能表上，選取**開啟專案**、 尋找.m2ssproj 專案檔中，選取檔案，並按一下**開啟**。  
  
2.  在重新連線到 MySQL**檔案**功能表上，選取**重新連接到 MySQL**。  
  
3.  若要重新連線到 SQL Server 上**檔案**功能表上，選取**重新連接到 SQL Server**。  
  
4.  若要重新連線到 SQL Azure 上**檔案**功能表上，選取**重新連線到 SQL Azure。**  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是[連接至 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
## <a name="see-also"></a>另請參閱  
[連接至 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
[移轉的 MySQL 資料庫到 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[連接到 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
[連接到 Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
