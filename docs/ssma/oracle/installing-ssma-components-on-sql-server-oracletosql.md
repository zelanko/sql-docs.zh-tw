---
title: SQL Server (OracleToSQL) 上安裝 SSMA 元件 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installign the Extension Pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 2041901a851ca755b1079535ccbf763472ec7bc4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47853356"
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>在 SQL Server 上安裝 SSMA 元件 (OracleToSQL)
除了安裝 SSMA，您必須也安裝元件正在執行的電腦上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 這些元件包括 SSMA 延伸模組套件，可支援資料移轉和 Oracle 提供者，以啟用伺服器對伺服器連線。  
  
## <a name="ssma-for-oracle-extension-pack"></a>SSMA for Oracle 延伸模組組件  
SSMA 延伸模組組件會加入資料庫中， **sysdb**並**ssmatesterdb**，以指定的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 資料庫**sysdb**包含資料表和預存程序，才能移轉資料，以及模擬 Oracle 系統函式的使用者定義函式。 **Ssmatesterdb**資料庫包含的資料表和程序所需的軟體測試人員元件。  
  
此外，當您將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，建立 SSMA[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式作業時，會使用伺服器端資料移轉引擎來移轉資料。  
  
### <a name="prerequisites"></a>先決條件  
您在上安裝 SSMA for Oracle 伺服器元件之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請確定系統符合下列需求：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝執行個體。 SSMA 不支援 SQL Server 2008 Express Edition。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更新版本。  
  
-   Oracle 用戶端提供者或 OLE DB provider for Oracle，並連線到您想要移轉的 Oracle 資料庫。 您可以從 Oracle 網站上的 Oracle 產品媒體安裝提供者。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務必須在安裝期間執行。 這用來填入清單的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在安裝精靈。 您可以停用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之後安裝的瀏覽器服務。  
  
    > [!NOTE]  
    > 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]瀏覽器服務正在執行，但您仍然看不見安裝程式中的執行個體的清單，您必須解除封鎖 UDP 通訊埠 1434年。 您可以使用 Windows 防火牆來暫時解除封鎖連接埠，或您可以暫時停用 Windows 防火牆。 您也可能會暫時停用防毒軟體。 請務必在安裝之後，啟用防火牆和防毒軟體。  
  
### <a name="installing-the-extension-pack"></a>安裝延伸模組組件  
您可以安裝的延伸模組組件之前您將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!IMPORTANT]  
> 若要安裝的延伸模組組件，您必須隸屬**sysadmin**伺服器角色的執行個體上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
**若要安裝的延伸模組組件**  
  
1.  如果您尚未這樣做，請從 SSMA Zip 檔案解壓縮所有檔案。  
  
    根據您所擁有的 WinZip 的版本，您可以按兩下檔案，或以滑鼠右鍵按一下檔案並選取**全部解壓縮**或是**WinZip 中開啟**。 遵循 WinZip 使用者介面中的指示，將檔案解壓縮。  
  
2.  複製 SSMA for Oracle 延伸模組套件。*n*。Install.exe，其中*n*是組建編號，來執行電腦[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
3.  按兩下 SSMA for Oracle 延伸模組套件。*n*。Install.exe。  
  
4.  在 歡迎使用 頁面上，按一下**下一步**。  
  
5.  在終端使用者授權合約 頁面上，閱讀授權合約。 如果您同意，請選取**我接受授權合約中的條款**核取方塊，然後按一下**下一步**。  
  
6.  在 [選擇安裝類型] 頁面上，按一下**典型**。  
  
7.  在 [準備安裝] 頁面上，按一下**安裝**。  
  
8.  在 [已完成安裝的第一個步驟] 頁面上，按一下 [**下一步]**。  
  
    新的對話方塊隨即出現，您可以在其中選取執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]延伸模組套件安裝。  
  
9. 選取的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]其中您要移轉 Oracle 結構描述，並再按**下一步**。  
  
    預設執行個體具有相同名稱的電腦。 具名執行個體將加上反斜線與執行個體名稱。  
  
10. 在 [連接] 頁面中，選取驗證方法，然後按一下 [**下一步]**。  
  
    Windows 驗證將用來嘗試登入的執行個體的 Windows 認證[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果您選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證，您必須輸入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入名稱和密碼。  
  
11. 在下一步 頁面上，選取**安裝公用程式資料庫** *n*，其中*n*是版本號碼，然後按一下**下一步**。  
  
    **Sysdb**會建立資料庫，並在該資料庫中建立的使用者定義函數和預存程序。  
  
    如果**安裝的軟體測試人員資料庫**選項會檢查軟體測試人員**ssmatesterdb**就會建立資料庫。  
  
12. 若要安裝的另一個執行個體的公用程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，選取 **[是]**，然後按一下**下一步**。 或者，若要結束精靈，請按一下**No**。  
  
13. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或藉由使用 sqlcmd 公用程式，執行下列指令碼，若要啟用 CLR:  
  
    ```  
    sp_configure 'clr enabled', 1  
    GO  
    RECONFIGURE  
    GO  
    ```  
    如果未啟用 CLR，您就會收到下列錯誤，當連接到的 SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    SSMA 無法擷取延伸模組組件的組件版本資訊。 資料庫伺服器上，重新安裝延伸模組套件。  
  
### <a name="sql-server-database-objects"></a>SQL Server 資料庫物件  
安裝延伸模組組件之後，您將會，請參閱**ssma_oracle.bcp_migration_packages**資料表**ssma_oracle.db_storage**資料表，和**ssma_oracle.db_error_list**資料表中**sysdb**資料庫。 您也會看到許多預存程序和使用者定義函數**ssma_oracle**結構描述。  
  
每當您將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，建立 SSMA[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式作業。 這些工作會命名為**ssma_oracle 資料移轉套件 {GUID}**，而且會出現在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式節點[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Jobs 資料夾中。  
  
## <a name="see-also"></a>另請參閱  
[安裝 SSMA for Oracle 用戶端&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[移轉的 Oracle 資料庫到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
