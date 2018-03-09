---
title: "安裝 SQL Server (SybaseToSQL) 上的 SSMA 元件 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
caps.latest.revision: "10"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d27ca7f0bc45c1d81118f0441d2ee4ff751d4c95
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>安裝 SQL Server (SybaseToSQL) 上的 SSMA 元件
除了安裝 SSMA，使用伺服器端資料移轉，您也必須安裝元件正在執行的電腦上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 這些元件包括 SSMA 延伸模組組件，可支援資料移轉和 Sybase 提供者，以啟用伺服器對伺服器的連線。  
  
## <a name="ssma-for-sybase-extension-pack"></a>SSMA for Sybase 延伸模組組件  
SSMA 延伸模組組件會加入資料庫， **sysdb**和**ssmatesterdb_syb**，以指定的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 **Sysdb**資料庫包含的資料表和資料移轉所需的預存程序。 **Ssmatester_syb**資料庫包含的結構描述**ssma_sybase_utilities**，SSMA tester 元件所使用的物件 （資料表、 觸發程序，檢視） 所建立。  
  
此外，當您將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，SSMA 建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理程式作業的伺服器端資料移轉引擎是用來進行資料移轉。  
  
### <a name="installing-the-extension-pack"></a>安裝擴充功能組件  
您可以安裝的延伸模組組件之前您移轉資料的任何時候[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
> [!IMPORTANT]  
> 若要安裝的延伸模組組件，您必須是執行個體上 sysadmin 伺服器角色的成員[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
**若要安裝的延伸模組組件**  
  
1.  複製 SSMA for Sybase 擴充套件。*n*.Install.exe 其中 *n* 為電腦執行的組建編號[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
2.  按兩下 SSMA for Sybase 擴充套件。*n*.Install.exe。  
  
3.  在 歡迎使用 頁面上，按一下 **下一步**。  
  
4.  在終端使用者授權合約 頁面上，閱讀授權合約。 如果您同意，請選取**我接受授權合約中的條款**核取方塊，然後**下一步**。  
  
5.  在 選擇安裝類型 頁面上，按一下 **一般**。  
  
6.  在 準備安裝 頁面上，按一下 **安裝**。  
  
7.  在已完成安裝的第一個步驟] 頁面上，按一下 [**下一步**。  
  
    新的對話方塊隨即出現，您可以在其中選取的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]擴充功能套件安裝。  
  
8.  選取的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]其中您將會移轉 ASE 資料庫，然後按一下**下一步**。  
  
    預設執行個體具有相同名稱的電腦。 具名執行個體將後面反斜線和執行個體名稱。  
  
9. 在連接參數] 頁面上，選取驗證方法，然後按一下 [**下一步**。  
  
    Windows 驗證會使用您的 Windows 認證來嘗試登入的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如果您選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]驗證，您必須輸入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]登入名稱和密碼。  
  
10. 在 [管理伺服器] 頁面上，選取**安裝公用程式資料庫**  *n* ，其中 *n* 是版本號碼，然後按一下**下一步**。  
  
    **Sysdb**建立資料庫和預存程序會建立該資料庫中。  
  
    如果**安裝軟體測試人員資料庫**選項會檢查軟體測試人員**ssmatesterdb_syb**就會建立資料庫。  
  
11. 若要安裝到其他執行個體的公用程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，選取**傳回執行個體**，然後按一下**下一步**。 或者，若要結束精靈，請按一下**結束**。  
  
### <a name="sql-server-database-objects"></a>SQL Server 資料庫物件  
安裝的延伸模組組件之後，您將會，請參閱**ssma_syb.bcp_migration_packages**資料表中**sysdb**資料庫。 您也會看到下列預存程序：  
  
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
  
每當您將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，SSMA 建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理程式作業。 這些作業會命名為**ssma_syb 資料移轉封裝 {GUID}**，而且會出現在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理程式節點[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]Jobs 資料夾中。  
  
## <a name="sybase-providers"></a>Sybase 的提供者  
當您將資料移轉至 ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SQL Azure 中，直接在 ASE 之間移轉資料和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SQL Azure。 它不會進出 SSMA 因為這會降低資料移轉。  
  
### <a name="installing-the-sybase-providers"></a>安裝的 Sybase 提供者  
下列指示會提供基本的安裝步驟來安裝 Sybase 提供者。 確切的指示將 Sybase 安裝程式的版本而有所不同。  
  
> [!IMPORTANT]  
> 執行安裝程式之前，請確認未違反您的授權合約。  
  
1.  執行 Sybase ASE 安裝程式。  
  
2.  選取 自訂安裝程式。  
  
3.  在 [功能選擇] 頁面中，選取 ODBC、 OLE DB 及 ADO.NET 資料提供者。  
  
4.  確認選取的功能，然後按一下**完成**安裝資料提供者。  
  
## <a name="see-also"></a>請參閱  
[安裝 SSMA for Sybase 用戶端 &#40;SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[Sybase ASE 將資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
