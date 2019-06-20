---
title: SQL Server (SybaseToSQL) 上安裝 SSMA 元件 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6121c75390e7493052a16b2e898eac69283e41ec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63294565"
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>在 SQL Server 上安裝 SSMA 元件 (SybaseToSQL)
除了安裝 SSMA，適用於使用伺服器端資料移轉，您必須也安裝元件正在執行的電腦上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 這些元件包括資料移轉以及若要啟用伺服器對伺服器連線的 Sybase 提供者所支援的 SSMA 延伸模組組件。  
  
## <a name="ssma-for-sybase-extension-pack"></a>SSMA for Sybase 延伸模組套件  
SSMA 延伸模組組件會加入資料庫中， **sysdb**並**ssmatesterdb_syb**，以指定的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 **Sysdb**資料庫包含的資料表和資料移轉所需的預存程序。 **Ssmatester_syb**資料庫包含的結構描述**ssma_sybase_utilities**，在其中 SSMA tester 元件所使用的物件 （資料表、 觸發程序，檢視） 會建立。  
  
此外，當您將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，建立 SSMA[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式作業時，會使用伺服器端資料移轉引擎來移轉資料。  
  
### <a name="installing-the-extension-pack"></a>安裝延伸模組組件  
您可以安裝的延伸模組組件之前您將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!IMPORTANT]  
> 若要安裝的延伸模組組件，您必須是 sysadmin 伺服器角色的成員執行個體上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
**若要安裝的延伸模組組件**  
  
1.  複製 SSMA for Sybase 延伸模組套件。*n*。Install.exe，其中*n*是組建編號，來執行電腦[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
2.  按兩下 SSMA for Sybase 延伸模組套件。*n*。Install.exe。  
  
3.  在 歡迎使用 頁面上，按一下**下一步**。  
  
4.  在終端使用者授權合約 頁面上，閱讀授權合約。 如果您同意，請選取**我接受授權合約中的條款**核取方塊，然後按一下**下一步**。  
  
5.  在 [選擇安裝類型] 頁面上，按一下**典型**。  
  
6.  在 [準備安裝] 頁面上，按一下**安裝**。  
  
7.  在 [已完成安裝的第一個步驟] 頁面上，按一下 [**下一步]** 。  
  
    新的對話方塊隨即出現，您可以在其中選取執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]延伸模組套件安裝。  
  
8.  選取的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您將會是 ASE 資料庫移轉，然後按一下**下一步**。  
  
    預設執行個體具有相同名稱的電腦。 具名執行個體將加上反斜線與執行個體名稱。  
  
9. 在 [連接參數] 頁面中，選取的驗證方法，然後按一下 [**下一步]** 。  
  
    Windows 驗證將用來嘗試登入的執行個體的 Windows 認證[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果您選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證，您必須輸入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入名稱和密碼。  
  
10. 在 管理伺服器 頁面上選取**安裝公用程式資料庫** *n*，其中*n*是版本號碼，然後按一下**下一步**。  
  
    **Sysdb**會建立資料庫，並在該資料庫中建立預存程序。  
  
    如果**安裝的軟體測試人員資料庫**選項會檢查軟體測試人員**ssmatesterdb_syb**就會建立資料庫。  
  
11. 若要安裝公用程式的另一個執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，選取**回到 執行個體**，然後按一下 **下一步]** 。 或者，若要結束精靈，請按一下**結束**。  
  
### <a name="sql-server-database-objects"></a>SQL Server 資料庫物件  
安裝延伸模組組件之後，您將會，請參閱**ssma_syb.bcp_migration_packages**資料表中**sysdb**資料庫。 您也會看到下列的預存程序：  
  
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
  
每當您將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，建立 SSMA[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式作業。 這些工作會命名為**ssma_syb 資料移轉套件 {GUID}** ，而且會出現在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式節點[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Jobs 資料夾中。  
  
## <a name="sybase-providers"></a>Sybase 提供者  
當您從 ASE，會在移轉資料時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ASE 之間的直接的 SQL Azure 資料移轉和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQL Azure。 它不會進出 SSMA 因為這可能會降低資料移轉速度。  
  
### <a name="installing-the-sybase-providers"></a>安裝的 Sybase 提供者  
下列指示安裝 Sybase 提供者提供的基本安裝步驟。 確切的指示將 Sybase 安裝程式的版本而有所不同。  
  
> [!IMPORTANT]  
> 執行安裝程式之前，請確認未違反您的授權合約。  
  
1.  執行 Sybase ASE 安裝程式。  
  
2.  選取 自訂安裝程式。  
  
3.  在 特徵選取 頁面中，選取 ODBC、 OLE DB 及 ADO.NET 資料提供者。  
  
4.  確認選取的功能，然後按一下**完成**安裝資料提供者。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for Sybase 用戶端&#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
