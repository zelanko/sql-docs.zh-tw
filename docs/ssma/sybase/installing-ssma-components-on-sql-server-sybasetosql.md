---
title: 在 SQL Server 上安裝 SSMA 元件（SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1fbc3a8f74b21bd5a53bdd874b5c41ef522e29f6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68029016"
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>在 SQL Server 上安裝 SSMA 元件 (SybaseToSQL)
除了安裝 SSMA 之外，若要使用伺服器端資料移轉，您也必須在執行的電腦上安裝元件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 這些元件包括支援資料移轉的 SSMA 延伸模組套件，以及可啟用伺服器對伺服器連線能力的 Sybase 提供者。  
  
## <a name="ssma-for-sybase-extension-pack"></a>Sybase 延伸模組套件的 SSMA  
SSMA 延伸模組套件會將資料庫**sysdb**和**ssmatesterdb_syb**加入至指定的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例。 **Sysdb**資料庫包含遷移資料所需的資料表和預存程式。 **Ssmatester_syb**資料庫包含架構**ssma_sybase_utilities**，其中會建立 ssma 測試器元件所使用的物件（資料表、觸發程式、Views）。  
  
此外，當您將資料移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]至時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA 會在伺服器端資料移轉引擎用於遷移資料時，建立 Agent 作業。  
  
### <a name="installing-the-extension-pack"></a>安裝延伸模組套件  
您可以在將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，隨時安裝延伸模組套件。  
  
> [!IMPORTANT]  
> 若要安裝延伸模組套件，您必須是實例上系統管理員（sysadmin）伺服器角色的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]成員。  
  
**安裝延伸模組套件**  
  
1.  複製 SSMA 的 Sybase 延伸模組套件。*n*。在執行的電腦上安裝 .exe，其中*n*是組建編號[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
2.  按兩下 [SSMA for Sybase Extension Pack]。*n*。安裝 .exe。  
  
3.  在 [歡迎] 頁面中按 [下一步]****。  
  
4.  在 [使用者授權合約] 頁面上，閱讀授權合約。 如果您同意，請選取 [**我接受授權合約中的條款**] 核取方塊，然後按 **[下一步]**。  
  
5.  在 [選擇安裝類型] 頁面上，按一下 [**一般**]。  
  
6.  在 [安裝準備就緒] 頁面上，按一下 [**安裝**]。  
  
7.  在 [完成安裝的第一個步驟] 頁面上，按 **[下一步]**。  
  
    此時會出現新的對話方塊，您可以在其中選取擴充功能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]套件安裝的實例。  
  
8.  選取您將在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]其中遷移 ASE 資料庫的實例，然後按 **[下一步]**。  
  
    預設實例與電腦具有相同的名稱。 命名實例後面會接著一個反斜線和實例名稱。  
  
9. 在 [連接參數] 頁面上，選取驗證方法，然後按 **[下一步]**。  
  
    Windows 驗證會使用您的 Windows 認證來嘗試登入的實例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果您選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [驗證]，則必須輸入登入名稱和密碼。  
  
10. 在 [管理伺服器] 頁面上，選取 [**安裝公用程式資料庫** *n*]，其中*n*是版本號碼，然後按 **[下一步]**。  
  
    系統會建立**sysdb**資料庫，並在該資料庫中建立預存程式。  
  
    如果已核取 [**安裝測試器資料庫**] 選項，則會建立**ssmatesterdb_syb**資料庫的測試人員。  
  
11. 若要將公用程式安裝到的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]另一個實例，請選取 [**返回實例**]，然後按 **[下一步]**。 或者，若要結束嚮導，請**按一下 [** 結束]。  
  
### <a name="sql-server-database-objects"></a>SQL Server 資料庫物件  
安裝延伸模組套件之後，您會在**sysdb**資料庫中看到**ssma_syb. bcp_migration_packages**資料表。 您也會看到下列預存程式：  
  
-   **bcp_clean_migration_data**  
  
-   **bcp_ensure_message_table**  
  
-   **bcp_insert_new_message**  
  
-   **bcp_post_process**  
  
-   **bcp_read_new_migration_messages**  
  
-   **bcp_save_migration_package**  
  
-   **bcp_smart_truncate**  
  
-   **bcp_start_migration_process**  
  
-   **get_jobstep_info**  
  
-   **stop_agent_process**  
  
每次您將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，SSMA 會[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]建立代理程式作業。 這些作業會命名為**ssma_syb 資料移轉封裝 {GUID}**，而且會顯示在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [作業] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]資料夾中的 [代理程式] 節點中。  
  
## <a name="sybase-providers"></a>Sybase 提供者  
當您將資料從 ASE 遷移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]至/SQL azure 時，資料會直接在 ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和/SQL azure 之間遷移。 它不會經過 SSMA，因為這會減緩資料移轉的速度。  
  
### <a name="installing-the-sybase-providers"></a>安裝 Sybase 提供者  
下列指示提供安裝 Sybase 提供者的基本安裝步驟。 確切的指示會根據 Sybase 安裝程式的版本而有所不同。  
  
> [!IMPORTANT]  
> 執行安裝程式之前，請確認您沒有違反授權合約。  
  
1.  執行 Sybase ASE 安裝程式。  
  
2.  選取 [自訂安裝]。  
  
3.  在 [特徵選取] 頁面上，選取 [ODBC]、[OLE DB] 和 [ADO.NET] 資料提供者。  
  
4.  確認選取的功能，然後按一下 **[完成]** 以安裝資料提供者。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for Sybase 用戶端 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
