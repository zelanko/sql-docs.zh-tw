---
title: 在 SQL Server 上安裝 SSMA 元件（OracleToSQL） |Microsoft Docs
description: 瞭解如何在執行 SQL Server 的電腦上安裝 SSMA 擴充功能套件和 Oracle 提供者，以支援 Oracle 資料庫轉換。
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installing the extension pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 2495d1b61b0251deee1b86ce66c03b6474f36cd8
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554823"
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>在 SQL Server 上安裝 SSMA 元件（OracleToSQL）

除了安裝 SSMA 以外，您也必須在執行的電腦上安裝元件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 這些元件包括支援資料移轉的 SSMA 延伸模組套件，以及可啟用伺服器對伺服器連線能力的 Oracle 提供者。

## <a name="ssma-for-oracle-extension-pack"></a>SSMA for Oracle 延伸模組套件

SSMA 延伸模組套件會將**sysdb**和**ssmatesterdb**資料庫加入至指定的實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 [資料庫**sysdb** ] 包含遷移資料所需的資料表和預存程式，以及模擬 Oracle 系統函數的使用者定義函數。 **Ssmatesterdb**資料庫包含測試人員元件所需的資料表和程式。

此外，當您將資料移轉至時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在伺服器端資料移轉引擎用於遷移資料時，建立 Agent 作業。

### <a name="prerequisites"></a>先決條件

在上安裝 SSMA for Oracle server 元件之前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請確定系統符合下列需求：

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例已安裝。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 或更新版本。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 版本4.7.2 或更新版本。 您可以從[.NET Framework 開發人員中心](https://go.microsoft.com/fwlink/?LinkId=48882)取得此檔案。
- 適用于 Oracle 的 OLE DB 提供者（如果使用 OLE DB），以及與您要遷移的 Oracle 資料庫之間的連接。 您可以從 Oracle 產品媒體或 Oracle 網站安裝提供者。
- 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間，Browser 服務必須正在執行。 這是用來 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在安裝精靈中填入實例的清單。 您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝後停用 Browser 服務。

  > [!NOTE]
  > 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務正在執行，但您仍然看不到安裝程式中的實例清單，則必須解除封鎖 UDP 埠1434。 您可以使用 Windows 防火牆暫時解除封鎖通訊埠，也可以暫時停用 Windows 防火牆。 您也可能需要暫時停用防毒軟體。 請務必在安裝後啟用防火牆和防毒軟體。

### <a name="installing-the-extension-pack"></a>安裝延伸模組套件

您可以隨時安裝延伸模組套件，然後再將資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。

> [!IMPORTANT]
> 若要安裝延伸模組套件，您必須是實例上**系統管理員（sysadmin** ）伺服器角色的成員 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。

若要安裝延伸模組套件：

1. 將**SSMAforOracleExtensionPack_*n*.msi** （其中*n*是組建編號）複製到執行的電腦 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。
2. 按兩下 [ **SSMAforOracleExtensionPack_*n*.msi**]。
3. 在 [歡迎]  頁面上，選取 [下一步]  。
4. 在 [**使用者授權合約**] 頁面上，閱讀授權合約。 如果您同意，請選取 **[我接受合約**] 選項，然後按 **[下一步]**。
5. 在 [**選擇安裝類型**] 頁面上，選取 [**一般**]。
6. 在 [已可安裝] **** 頁面上，選取 [安裝] ****。
7. 在 [**完成安裝的第一個步驟**] 頁面上，選取 **[下一步]**。
  
   新的對話方塊隨即出現。 選取擴充功能套件類型。
  
8. 選取所需的安裝類型，然後按 **[下一步]**。

   > [!IMPORTANT]
   > 只有在安裝擴充功能套件時，或以為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目標時，才使用遠端選項 [!INCLUDE[ssAzureMi](../../includes/ssazuremi_md.md)] 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在 Windows 上執行的安裝應該一律在本機安裝延伸模組套件。 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]和 Azure SQL 資料倉儲不支援延伸模組套件。

   如果您要在本機實例上安裝延伸模組套件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則下一個頁面將可讓您選擇要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在其中遷移 Oracle 架構的本機實例。 在下拉式選單中選擇實例，然後選取 **[下一步]**。

   預設實例與電腦具有相同的名稱。 命名實例後面會接著一個反斜線和實例名稱。

9. 在 [連接] 頁面上，選取驗證方法，然後選取 **[下一步]**。

   Windows 驗證會使用您的 Windows 認證嘗試登入的實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果您選取 [伺服器驗證]，則必須輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱和密碼。

10. 接下來，您必須設定主要金鑰的密碼，以便在伺服器端資料移轉期間，用來加密儲存在延伸模組套件資料庫中的任何敏感性資料。 提供強式密碼，然後按 **[下一步]**。

11. 在下一個頁面上，選取 [**安裝公用程式資料庫*n*並安裝延伸模組套件程式庫**]，其中*n*是版本號碼。 如果您計畫使用測試器功能，請選取 [**安裝測試人員資料庫**] 核取方塊，然後選取 **[下一步]**。

    系統會使用在此資料庫中建立資料移轉所需的資料表和預存程式（使用伺服器端資料移轉引擎）來建立**sysdb**資料庫。

    如果核取 [**安裝測試器資料庫**] 選項，將會建立**ssmatesterdb**資料庫。

12. 安裝完成之後，會出現提示，詢問您是否要在另一個實例上安裝公用程式資料庫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，選取 **[是**]，然後選取 **[下一步**]，或是結束嚮導，選取 [ ** ****否**]，然後選取 [結束]。

13. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或中使用 `sqlcmd` 公用程式，執行下列腳本來啟用 CLR：

    ```sql
    sp_configure 'clr enabled', 1
    GO
    RECONFIGURE
    GO
    ```

    如果 CLR 未啟用，當 SSMA 連接到時，您會收到下列錯誤 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ：

    > SSMA 無法捕獲延伸模組元件的版本資訊。 在資料庫伺服器上重新安裝延伸模組套件。

### <a name="sql-server-database-objects"></a>SQL Server 資料庫物件

安裝延伸模組套件之後，[ **ssma_oracle] bcp_migration_packages**資料表會出現在**sysdb**資料庫中。

每次您將資料移轉至時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，SSMA 會建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式作業。 這些作業會命名為**ssma_oracle 資料移轉封裝 {GUID}**，而且會顯示在 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 作業] 資料夾中的 [代理程式] 節點中 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。

## <a name="see-also"></a>另請參閱

- [安裝 SSMA for Oracle 用戶端](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)
- [將 Oracle 資料庫移轉到 SQL Server](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)
