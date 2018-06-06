---
title: 安裝 SQL Server (OracleToSQL) 上的 SSMA 元件 |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Installign the Extension Pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: d75694edf4af06ec2d1e442ecebacaf971ba86de
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>安裝 SQL Server (OracleToSQL) 上的 SSMA 元件
除了安裝 SSMA，您也必須安裝元件正在執行的電腦上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 這些元件包括 SSMA 延伸模組組件，可支援資料移轉和 Oracle 提供者，以啟用伺服器對伺服器的連線。  
  
## <a name="ssma-for-oracle-extension-pack"></a>SSMA for Oracle 延伸模組組件  
SSMA 延伸模組組件會加入資料庫， **sysdb**和**ssmatesterdb**，以指定的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 資料庫**sysdb**包含資料表和預存程序所需移轉資料，以及模擬 Oracle 系統函數的使用者定義函數。 **Ssmatesterdb**資料庫包含的資料表和程序所需的測試人員元件。  
  
此外，當您將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，SSMA 建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理程式作業的伺服器端資料移轉引擎是用來進行資料移轉。  
  
### <a name="prerequisites"></a>필수 구성 요소  
SSMA for Oracle 伺服器元件在安裝之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，請確定系統符合下列需求：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 安裝執行個體。 SSMA 不支援 SQL Server 2008 Express Edition。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更新版本。  
  
-   Oracle 用戶端提供者或 OLE DB provider for Oracle 和您想要移轉的 Oracle 資料庫的連接。 您可以從 Oracle 產品媒體或 Oracle 網站上安裝提供者。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]瀏覽器服務必須在安裝期間執行。 這用來填入清單的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]在安裝精靈。 您可以停用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]之後安裝的瀏覽器服務。  
  
    > [!NOTE]  
    > 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]瀏覽器服務正在執行，但您仍然看不在安裝程式中的執行個體的清單，您必須解除封鎖 UDP 通訊埠 1434年。 您可以使用 Windows 防火牆來暫時解除封鎖通訊埠，或您可以暫時停用 Windows 防火牆。 您也可能必須暫時停用防毒軟體。 請務必在安裝之後啟用防火牆和防毒軟體。  
  
### <a name="installing-the-extension-pack"></a>安裝擴充功能組件  
您可以安裝的延伸模組組件之前您移轉資料的任何時候[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
> [!IMPORTANT]  
> 若要安裝的延伸模組組件，您必須是成員**sysadmin**伺服器角色的執行個體上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
**若要安裝的延伸模組組件**  
  
1.  如果您尚未這樣做，請從 SSMA Zip 檔案解壓縮所有檔案。  
  
    根據您所擁有的 WinZip 版本，您可以按兩下該檔案，或以滑鼠右鍵按一下該檔案並選取**全部解壓縮**或**WinZip 中開啟**。 依照 WinZip 使用者介面中的指示，將檔案解壓縮。  
  
2.  複製 SSMA for Oracle 延伸模組組件。*n*。Install.exe 其中*n*為電腦執行的組建編號[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
3.  按兩下 SSMA for Oracle 延伸模組組件。*n*。Install.exe。  
  
4.  在 歡迎使用 頁面上，按一下 **下一步**。  
  
5.  在終端使用者授權合約 頁面上，閱讀授權合約。 如果您同意，請選取**我接受授權合約中的條款**核取方塊，然後**下一步**。  
  
6.  在 選擇安裝類型 頁面上，按一下 **一般**。  
  
7.  在 準備安裝 頁面上，按一下 **安裝**。  
  
8.  在已完成安裝的第一個步驟] 頁面上，按一下 [**下一步**。  
  
    新的對話方塊隨即出現，您可以在其中選取的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]擴充功能套件安裝。  
  
9. 選取的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]其中您將會移轉 Oracle 結構描述，然後再按一下**下一步**。  
  
    預設執行個體具有相同名稱的電腦。 具名執行個體將後面反斜線和執行個體名稱。  
  
10. 在 連接 頁面上選取驗證方法，然後按一下 **下一步**。  
  
    Windows 驗證會使用您的 Windows 認證來嘗試登入的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如果您選取[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]驗證，您必須輸入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]登入名稱和密碼。  
  
11. 在下一個頁面上，選取**安裝公用程式資料庫** *n*，其中*n*是版本號碼，然後按一下**下一步**。  
  
    **Sysdb**建立資料庫，並在該資料庫中建立的使用者定義函數和預存程序。  
  
    如果**安裝軟體測試人員資料庫**選項會檢查軟體測試人員**ssmatesterdb**就會建立資料庫。  
  
12. 若要安裝到其他執行個體的公用程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，選取**是**，然後按一下 **下一步**。 或者，若要結束精靈，請按一下**否**。  
  
13. 在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]或使用 sqlcmd 公用程式，執行下列指令碼，若要啟用 CLR:  
  
    ```  
    sp_configure 'clr enabled', 1  
    GO  
    RECONFIGURE  
    GO  
    ```  
    如果未啟用 CLR，您會收到下列錯誤，當 SSMA 連線到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:  
  
    SSMA 無法擷取的延伸模組組件的組件版本資訊。 資料庫伺服器上，重新安裝擴充功能組件。  
  
### <a name="sql-server-database-objects"></a>SQL Server 資料庫物件  
安裝的延伸模組組件之後，您將會，請參閱**ssma_oracle.bcp_migration_packages**資料表**ssma_oracle.db_storage**資料表，和**ssma_oracle.db_error_list**資料表中**sysdb**資料庫。 您也會看到許多預存程序和使用者定義函數中的**ssma_oracle**結構描述。  
  
每當您將資料移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，SSMA 建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理程式作業。 這些作業會命名為**ssma_oracle 資料移轉封裝 {GUID}**，而且會出現在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理程式節點[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]Jobs 資料夾中。  
  
## <a name="see-also"></a>另請參閱  
[安裝 Oracle 用戶端的 SSMA &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[SQL server 資料庫移轉 Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
