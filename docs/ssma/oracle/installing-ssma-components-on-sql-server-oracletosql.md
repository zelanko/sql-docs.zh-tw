---
title: 在 SQL Server 上安裝 SSMA 元件（OracleToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 10/01/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installign the Extension Pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 1f0cea859e9465eebefebc061ee51107dc7844aa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "71713315"
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>在 SQL Server 上安裝 SSMA 元件（OracleToSQL）

除了安裝 SSMA 以外，您也必須在執行的電腦上安裝元件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 這些元件包括支援資料移轉的 SSMA 延伸模組套件，以及可啟用伺服器對伺服器連線能力的 Oracle 提供者。  
  
## <a name="ssma-for-oracle-extension-pack"></a>SSMA for Oracle 延伸模組套件

SSMA 延伸模組套件會將**sysdb**和**ssmatesterdb**資料庫加入至指定的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例。 [資料庫**sysdb** ] 包含遷移資料所需的資料表和預存程式，以及模擬 Oracle 系統函數的使用者定義函數。 **Ssmatesterdb**資料庫包含測試人員元件所需的資料表和程式。  
  
此外，當您將資料移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]至時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA 會在伺服器端資料移轉引擎用於遷移資料時，建立 Agent 作業。  
  
### <a name="prerequisites"></a>Prerequisites

在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝 SSMA for Oracle server 元件之前，請確定系統符合下列需求：  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例已安裝。 SSMA 不支援 SQL Server 2008 Express Edition。
  
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 或更新版本。  
  
- Oracle 用戶端提供者或 Oracle 的 OLE DB 提供者，以及您要遷移之 Oracle 資料庫的連接。 您可以從 Oracle 產品媒體或 Oracle 網站安裝提供者。  
  
- 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝期間，Browser 服務必須正在執行。 這是用來在安裝精靈中填入實例的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]清單。 您可以在安裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]後停用 Browser 服務。  
  
    > [!NOTE]  
    > 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務正在執行，但您仍然看不到安裝程式中的實例清單，則必須解除封鎖 UDP 埠1434。 您可以使用 Windows 防火牆暫時解除封鎖通訊埠，也可以暫時停用 Windows 防火牆。 您也可能需要暫時停用防毒軟體。 請務必在安裝後啟用防火牆和防毒軟體。  
  
### <a name="installing-the-extension-pack"></a>安裝延伸模組套件

您可以隨時安裝延伸模組套件，然後再將資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]遷移至。  
  
> [!IMPORTANT]  
> 若要安裝延伸模組套件，您必須是實例上**系統管理員（sysadmin** ）伺服器角色的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]成員。  
  
**安裝延伸模組套件**
  
1. 如果您還沒有這麼做，請從 SSMA Zip 檔案解壓縮所有檔案。  
  
    視您擁有的 WinZip 版本而定，您可以按兩下檔案，或以滑鼠右鍵按一下檔案，然後選取 [**全部解壓縮**] 或 [**在 WinZip 中開啟**]。 依照 [WinZip] 使用者介面中的指示來解壓縮檔案。  
  
2. 複製**SSMA For Oracle 延伸模組套件。*n*。** 在執行的電腦上安裝 .exe （其中*n*是組建編號） [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
3. 按兩下 [ **SSMA For Oracle Extension Pack]。*n*。安裝 .exe**。  
  
4. 在 [歡迎]  頁面上，選取 [下一步]  。  
  
5. 在 [**使用者授權合約**] 頁面上，閱讀授權合約。 如果您同意，請選取 [**我接受授權合約中的條款**] 核取方塊，然後選取 **[下一步]**。  
  
6. 在 [**選擇安裝類型**] 頁面上，選取 [**一般**]。  
  
7. 在 [已可安裝] **** 頁面上，選取 [安裝] ****。  
  
8. 在 [**完成安裝的第一個步驟**] 頁面上，選取 **[下一步]**。  
  
    此時會出現新的對話方塊，您可以在其中選取擴充功能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]套件安裝的實例。  
  
9. 選取您要在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]其中遷移 Oracle 架構的實例，然後選取 **[下一步]**。  
  
    預設實例與電腦具有相同的名稱。 命名實例後面會接著一個反斜線和實例名稱。  
  
10. 在 [連接] 頁面上，選取驗證方法，然後選取 **[下一步]**。  
  
    Windows 驗證會使用您的 Windows 認證嘗試登入的實例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果您選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [驗證]，則必須輸入登入名稱和密碼。  
  
11. 在下一個頁面上，選取 [**安裝公用程式資料庫** *n*]，其中*n*是版本號碼，然後選取 **[下一步]**。  
  
    系統會建立**sysdb**資料庫，並在該資料庫中建立使用者定義函數和預存程式。  
  
    如果核取 [**安裝測試器資料庫**] 選項，將會建立測試人員**ssmatesterdb**資料庫。  
  
12. 若要將公用程式安裝到另[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]一個實例，請選取 **[是]**，然後選取 **[下一步**]，或者若要結束嚮導，請選取 [**否**]。  
  
13. 在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或中使用 sqlcmd 公用程式，執行下列腳本來啟用 CLR：  
  
    ```
    sp_configure 'clr enabled', 1  
    GO  
    RECONFIGURE  
    GO  
    ```

    如果 CLR 未啟用，當 SSMA 連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，您會收到下列錯誤：  
  
    SSMA 無法捕獲延伸模組元件的版本資訊。 在資料庫伺服器上重新安裝延伸模組套件。  
  
### <a name="sql-server-database-objects"></a>SQL Server 資料庫物件  

安裝延伸模組套件之後，[ **ssma_oracle] bcp_migration_packages**資料表會出現在**sysdb**資料庫中。

每次您將資料移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]至時，SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會建立代理程式作業。 這些作業會命名為**ssma_oracle 資料移轉封裝 {GUID}**，而且會顯示在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [作業] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]資料夾中的 [代理程式] 節點中。  
  
## <a name="see-also"></a>另請參閱

[安裝 SSMA for Oracle Client &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[將 Oracle 資料庫移轉至 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
