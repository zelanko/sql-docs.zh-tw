---
title: 在 SQL Server (OracleToSQL) 上安裝 SSMA 元件 |Microsoft Docs
description: 瞭解如何在執行 SQL Server 的電腦上安裝 SSMA 擴充功能套件和 Oracle 提供者，以支援 Oracle 資料庫轉換。
ms.prod: sql
ms.custom: ''
ms.date: 11/16/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installing the extension pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 64850d1a701491f0dc5817576a568fdc3ebc2483
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870096"
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>在 SQL Server (OracleToSQL) 上安裝 SSMA 元件

除了安裝 SSMA 之外，您也必須在執行的電腦上安裝元件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 這些元件包括支援資料移轉的 SSMA 延伸模組套件，以及可啟用伺服器對伺服器連線能力的 Oracle 提供者。

## <a name="ssma-for-oracle-extension-pack"></a>SSMA for Oracle 擴充功能套件

SSMA 延伸模組套件會部署擴充預存程式，並將 **sysdb** 和 **ssmatesterdb** 資料庫加入至指定的實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 擴充預存程式提供模擬 Oracle 功能和 behaiov 所需的功能，而 **sysdb** 資料庫則包含遷移資料所需的資料表和預存程式。 **Ssmatesterdb** 資料庫包含測試人員元件 (（如果已安裝) ）所需的資料表和程式。

此外，當您將資料移轉至時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在使用伺服器端資料移轉引擎來遷移資料時建立代理程式作業。

### <a name="prerequisites"></a>先決條件

在上安裝 SSMA for Oracle server 元件之前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請確定系統符合下列需求：

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已安裝實例。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更新版本。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 版本4.7.2 或更新版本。 您可以從 [.NET Framework 開發人員中心](https://go.microsoft.com/fwlink/?LinkId=48882)取得。
- 如果使用 OLE DB) ，以及您想要遷移的 Oracle 資料庫的連接，則 OLE DB 的 Oracle provider (。 您可以從 Oracle 產品媒體或 Oracle 網站安裝提供者。
- 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間，瀏覽器服務必須正在執行。 這是用來 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 [安裝精靈] 中填入實例清單。 您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝後停用瀏覽器服務。

  > [!NOTE]
  > 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務正在執行中，但您仍然沒有在安裝程式中看到實例清單，則必須解除封鎖 UDP 埠1434。 您可以使用 Windows 防火牆暫時解除封鎖埠，也可以暫時停用 Windows 防火牆。 您可能也必須暫時停用防毒軟體。 安裝之後，請務必啟用防火牆和防毒軟體。

### <a name="installing-the-extension-pack"></a>安裝延伸模組套件

您可以在將資料移轉至之前，隨時安裝擴充套件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。

> [!IMPORTANT]
> 若要安裝擴充功能套件，您必須是實例上 **系統管理員（sysadmin** ）伺服器角色的成員 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。

若要安裝延伸模組套件：

1. 複製 **SSMAforOracleExtensionPack_ *n*** 的 (，其中 *n* 是) 到執行之電腦的組建編號。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
2. 按兩下 [ **SSMAforOracleExtensionPack_ *n*.msi**。
3. 在 [歡迎使用]  頁面，按 [下一步]  。
4. 在 [ **使用者授權合約** ] 頁面上，閱讀授權合約。 如果您同意，請選取 **[我接受合約** ] 選項，然後按 **[下一步]**。
5. 在 [ **選擇安裝類型** ] 頁面上，選取 [ **一般**]。
6. 在 [已可安裝]  頁面上，選取 [安裝] 。
7. 在 [ **完成安裝的第一個步驟** ] 頁面上，選取 **[下一步]**。
  
   新的對話方塊隨即出現。 選取延伸模組套件類型。
  
8. 選取所需的安裝類型，然後按 **[下一步]**。

   > [!IMPORTANT]
   > 只有在 Linux 上執行的延伸模組或以目標為目標時，才應使用 Remote 選項 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzureMi](../../includes/ssazuremi_md.md)] 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 Windows 上執行的安裝應該一律在本機安裝延伸模組套件。 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 和 Azure Synapse Analytics 不支援延伸模組套件。

   如果您要在本機實例上安裝擴充功能套件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則下一個頁面將可讓您選擇要將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle 架構遷移至其中的本機實例。 在下拉式清單中選擇實例，然後選取 **[下一步]**。

   預設實例的名稱與電腦相同。 命名的實例後面會接著反斜線和實例名稱。

9. 在 [連接] 頁面上，選取驗證方法，然後選取 **[下一步]**。

   Windows 驗證會使用您的 Windows 認證來嘗試登入的實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果您選取 [伺服器驗證]，就必須輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱和密碼。

10. 下一個步驟會要求您設定主要金鑰的密碼，在伺服器端資料移轉期間，將用來加密儲存在延伸模組套件資料庫中的任何敏感性資料。 提供強式密碼，然後按 **[下一步]**。

11. 在下一個頁面上，選取 [ **安裝公用程式資料庫 *n* ] 並安裝延伸套件程式庫**，其中 *n* 是版本號碼。 如果您計畫使用測試人員功能，請選取 [ **安裝測試人員資料庫** ] 核取方塊，然後選取 **[下一步]**。

    **Sysdb** 資料庫是使用資料移轉所需的資料表和預存程式所建立， (使用伺服器端資料移轉引擎) 在此資料庫中建立的。

    如果選取 [ **安裝測試人員資料庫** ] 選項，則會建立 **ssmatesterdb** 資料庫。

12. 安裝完成之後，會出現提示，詢問您是否要在的另一個實例上安裝公用程式資料庫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、選取 **[是]**，然後選取 **[下一步**]，或是結束嚮導，請 **Exit** 選取 [**否**]，然後選取 [結束]。

13. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或中使用 `sqlcmd` 公用程式，執行下列腳本以啟用 CLR：

    ```sql
    sp_configure 'clr enabled', 1
    GO
    RECONFIGURE
    GO
    ```

    如果未啟用 CLR，當 SSMA 連接至時，您將會收到下列錯誤 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ：

    > SSMA 無法抓取延伸模組元件的版本資訊。 在資料庫伺服器上重新安裝延伸模組套件。

### <a name="sql-server-database-objects"></a>SQL Server 資料庫物件

在您安裝延伸模組套件之後， **sysdb** 資料庫中就會出現 **ssma_oracle 的 bcp _migration_packages** 資料表。

每次您將資料移轉至時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，SSMA 會建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式作業。 這些作業會命名為 **ssma_oracle 資料移轉封裝 {GUID}**，而且會顯示在 [作業] 資料夾的 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式] 節點中 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。

此外，也會將下列擴充預存程式加入至 **master** 資料庫：

- `xp_ora2ms_exec2`
- `xp_ora2ms_exec2_ex`
- `xp_ora2ms_versioninfo2`

## <a name="see-also"></a>請參閱

- [安裝 SSMA for Oracle 用戶端](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)
- [將 Oracle 資料庫移轉到 SQL Server](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)
