---
description: 在 SQL Server (SybaseToSQL) 上安裝 SSMA 元件
title: 在 SQL Server (SybaseToSQL) 上安裝 SSMA 元件 |Microsoft Docs
ms.custom: ''
ms.date: 07/14/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 33b5663e7693de8c031f2b39c0436a771920be56
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88372364"
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>在 SQL Server (SybaseToSQL) 上安裝 SSMA 元件

除了安裝 SSMA 之外，若要使用伺服器端資料移轉，您也必須在執行的電腦上安裝元件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 這些元件包括支援資料移轉的 SSMA 延伸模組套件，以及可啟用伺服器對伺服器連線能力的 Sybase 提供者。

## <a name="ssma-for-sybase-extension-pack"></a>SSMA for Sybase extension pack

SSMA 延伸套件會將資料庫（ **sysdb** 和 **ssmatesterdb_syb**）加入至指定的實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 **Sysdb**資料庫包含資料移轉所需的資料表和預存程式。 **Ssmatester_syb**資料庫包含架構**ssma_sybase_utilities**，其中會建立 ssma 測試器元件所使用的物件 (資料表、觸發程式、視圖) 。

此外，當您將資料移轉至時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在使用伺服器端資料移轉引擎來遷移資料時建立代理程式作業。

### <a name="prerequisites"></a>先決條件

在上安裝適用于 Sybase 伺服器元件的 SSMA 之前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請確定系統符合下列需求：

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已安裝實例。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更新版本。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 版本4.7.2 或更新版本。 您可以從 [.NET Framework 開發人員中心](https://go.microsoft.com/fwlink/?LinkId=48882)取得。
- Sybase OLE DB/ADO.Net/ODBC 提供者，以及包含您想要遷移之資料庫的 SAP ASE 資料庫伺服器的連線能力。 您可以從 SAP ASE 產品媒體安裝提供者。 如需連線的詳細資訊，請參閱 [連接到 SYBASE ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)。
- 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間，瀏覽器服務必須正在執行。 這是用來 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 [安裝精靈] 中填入實例清單。 您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝後停用瀏覽器服務。

  > [!NOTE]
  > 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務正在執行中，但您仍然沒有在安裝程式中看到實例清單，則必須解除封鎖 UDP 埠1434。 您可以使用 Windows 防火牆暫時解除封鎖埠，也可以暫時停用 Windows 防火牆。 您可能也必須暫時停用防毒軟體。 安裝之後，請務必啟用防火牆和防毒軟體。

### <a name="installing-the-extension-pack"></a>安裝延伸模組套件

您可以在將資料移轉至之前，隨時安裝延伸模組套件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。

> [!IMPORTANT]
> 若要安裝擴充功能套件，您必須是實例上系統管理員（sysadmin）伺服器角色的成員 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。

若要安裝延伸模組套件：

1. 將 **SSMAforSybaseExtensionPack_*n*.msi**（其中 *n* 是組建編號）複製到正在執行的電腦 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。
2. 按兩下 [ **SSMAforSybaseExtensionPack_*n*.msi**。
3. 在 [歡迎] 頁面中按 [下一步]。
4. 在 [ **使用者授權合約** ] 頁面上，閱讀授權合約。 如果您同意，請選取 [ **我接受合約** ] 選項，然後按 [ **下一步]**。
5. 在 [ **選擇安裝類型** ] 頁面上，按一下 [ **一般**]。
6. 在 [ **安裝準備就緒** ] 頁面上，按一下 [ **安裝**]。
7. 在 [ **完成安裝的第一個步驟** ] 頁面上，按 **[下一步]**。

   新的對話方塊隨即出現，您可以在其中選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 擴充功能套件安裝的實例。

8. 選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 您將在其中遷移 SAP ASE 資料庫的實例，然後按 **[下一步]**。

   預設實例的名稱與電腦相同。 命名的實例後面會接著反斜線和實例名稱。

9. 在 [連接] 頁面上，選取驗證方法，然後按 **[下一步]**。

   Windows 驗證會使用您的 Windows 認證來嘗試登入的實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果您選取 [伺服器驗證]，就必須輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱和密碼。

10. 下一個步驟會要求您設定主要金鑰的密碼，在伺服器端資料移轉期間，將用來加密儲存在延伸模組套件資料庫中的任何敏感性資料。 提供強式密碼，然後按 **[下一步]**。

11. 在下一個頁面上，選取 [ **安裝公用程式資料庫 *n* ] 並安裝延伸套件程式庫**，其中 *n* 是版本號碼。 如果您計畫使用測試人員功能，請選取 [ **安裝測試人員資料庫** ] 核取方塊，然後選取 **[下一步]**。

    **Sysdb**資料庫是使用資料移轉所需的資料表和預存程式所建立， (使用伺服器端資料移轉引擎) 在此資料庫中建立的。

    如果選取 [ **安裝測試人員資料庫** ] 選項，則會建立 **ssmatesterdb_syb** 資料庫。

12. 安裝完成之後，會出現提示，詢問您是否要在的另一個實例上安裝公用程式資料庫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、選取 **[是]**，然後選取 **[下一步**]，或是結束嚮導，請**Exit**選取 [**否**]，然後選取 [結束]。

### <a name="sql-server-database-objects"></a>SQL Server 資料庫物件

安裝延伸模組套件之後，您會在**sysdb**資料庫中看到**ssma_syb 的 bcp_migration_packages**資料表。 您也會看到下列預存程式：

- `bcp_clean_migration_data`
- `bcp_ensure_message_table`
- `bcp_insert_new_message`
- `bcp_post_process`
- `bcp_read_new_migration_messages`
- `bcp_save_migration_package`
- `bcp_smart_truncate`
- `bcp_start_migration_process`
- `get_jobstep_info`
- `stop_agent_process`

每次您將資料移轉至時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，SSMA 會建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式作業。 這些作業會命名為 **ssma_syb 資料移轉封裝 {GUID}**，而且會顯示在 [作業] 資料夾的 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式] 節點中 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。  

## <a name="sybase-providers"></a>Sybase 提供者

當您使用伺服器端資料移轉將資料從 SAP ASE 移至時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，資料會直接在 SAP ase 和之間遷移 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 它不會經過 SSMA，因為這會減緩資料移轉的速度。

### <a name="installing-the-sybase-providers"></a>安裝 Sybase 提供者

下列指示提供安裝 Sybase 提供者的基本安裝步驟。 確切的指示會根據 Sybase 安裝程式的版本而有所不同。

> [!IMPORTANT]
> 執行安裝程式之前，請確認您不違反授權合約。

1. 執行 Sybase ASE 安裝程式。
2. 選取 [自訂安裝]。
3. 在 [特徵選取] 頁面上，選取 [ODBC]、[OLE DB] 和 [ADO.NET] 資料提供者。
4. 確認選取的功能，然後按一下 **[完成]** 以安裝資料提供者。

## <a name="see-also"></a>另請參閱

- [安裝適用于 Sybase 用戶端的 SSMA](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)
- [將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL Database](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)
