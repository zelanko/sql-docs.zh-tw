---
title: 執行 DQSInstaller.exe 完成 Data Quality Server 安裝 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7a8c96e0-1328-4f35-97fc-b6d9cb808bae
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c80d7ab755580bece61606c658c8603cd76c3b55
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131794"
---
# <a name="run-dqsinstallerexe-to-complete-data-quality-server-installation"></a>執行 DQSInstaller.exe 完成 Data Quality Server 安裝
  若要完成 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 安裝，您必須在安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]之後，執行 DQSInstaller.exe 檔案。 本主題描述如何從 **[開始]** 畫面、 **[開始]** 功能表、Windows [檔案總管] 或 [命令提示字元] 執行 DQSInstaller.exe。您可以任選一種方法執行 DQSInstaller.exe 檔案。  
  
##  <a name="Prerequisites"></a> 必要條件  
  
-   安裝 SQL Server 時，必須先在 SQL Server 設定的 [特徵選取] 頁面中，選取 **[Database Engine Services]** 之下的 **[Data Quality Services]** ，而且必須先完成 SQL Server 安裝。 如需詳細資訊，請參閱 [安裝 Data Quality Services](install-data-quality-services.md)。  
  
-   您的 Windows 使用者帳戶必須是 SQL Server 資料庫引擎執行個體上系統管理員 (sysadmin) 固定伺服器角色的成員。  
  
-   您必須以您要執行 DQSInstaller.exe 所在電腦上的管理員群組成員的身分登入。  
  
##  <a name="WindowsExplorer"></a> 從 [開始] 畫面、[開始] 功能表或 Windows 檔案總管執行 DQSInstaller.exe  
  
1.  在您選擇要安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]的電腦上，使用下列任一適用的方法執行 DQSInstaller.exe 檔案：  
  
    -   **開始畫面**：在 **[開始]** 畫面上，按一下 **[資料品質伺服器安裝程式]**  
  
    -   **開始功能表**：在工作列上，按一下 **[開始]**，指向 **[所有程式]**，然後按一下 **[Microsoft SQL Server 2014]**。 在 **[Microsoft SQL Server 2014]** 底下按一下 **[Data Quality Services]**，然後按一下 **[Data Quality Server Installer]**。  
  
    -   **Windows 檔案總管**：尋找 DQSInstaller.exe 檔。 如果已經安裝了 SQL Server 的預設執行個體，DQSInstaller.exe 檔案將會位於 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn。 按兩下 DQSInstaller.exe 檔案。  
  
2.  命令提示字元視窗會隨即出現，並顯示安裝狀態。 您將發現下列三種情況：  
  
    1.  安裝程式會建立內含執行 DQSInstaller.exe 檔案時所執行之動作相關資訊的 DQS_install.log 安裝記錄檔。 您如果安裝了 SQL Server 的預設執行個體，DQS_install.log 檔案將會位於 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Log。  
  
    2.  安裝程式會使用預設伺服器定序 SQL_Latin1_General_CP1_CI_AS 安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]。  
  
        > [!IMPORTANT]  
        >  只有從命令提示字元執行 DQSInstaller.exe 時，才能提供不同的伺服器定序值來安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 。 如需詳細資訊，請參閱本主題稍後的＜ [從命令提示字元執行 DQSInstaller.exe](#CommandPrompt) ＞。  
  
    3.  安裝程式會檢查電腦是否因最近安裝的任何更新而有任何暫止的重新啟動。 如果發現任何暫止的重新啟動，則會出現一則訊息通知您這種情況，您可以分別按下 Y 或 N，選擇繼續或中止安裝。 我們建議您，如果有任何暫止的重新啟動，則必須中止安裝、重新啟動電腦，然後再次執行 DQSInstaller.exe。  
  
3.  您會收到提示要求您輸入資料庫主要金鑰的密碼。 稍後當您在 [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) 中設定參考資料庫提供者時，必須使用資料庫主要金鑰加密參考資料服務提供者金鑰，而此金鑰將儲存在 DQS_MAIN 資料庫中。  
  
    > [!IMPORTANT]  
    >  密碼的長度至少必須是 8 個字元，且必須包含下列四種類別的其中三種字元：英文大寫字母  (A、B、C… Z)、英文小寫字母 (a、b、c... z)、數字 (0、1、2... 9)，以及非英數或特殊字元 (~!@#$%^&*()_-+=|\\{}[]:;"'<>,.?/)。 例如： P@ssword＞。 如果目前的密碼不符合要求，安裝程式將會提示您輸入其他密碼。  
  
4.  請提供並確認密碼，然後按 ENTER 繼續安裝。  
  
    > [!IMPORTANT]  
    >  您必須保留針對資料庫主要金鑰所指定的密碼，因為如果您將來選擇從備份還原 DQS 資料庫，您將需要此密碼。 如需有關還原 DQS 資料庫的詳細資訊，請參閱＜ [Backing Up and Restoring DQS Databases](../backing-up-and-restoring-dqs-databases.md)＞。  
  
5.  如果 Master Data Services 當做 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]，存在於相同的 SQL Server 執行個體中，則安裝程式會建立對應到 Master Data Services 登入的使用者，並且授與該使用者 DQS_MAIN 資料庫的 dqs_administrator 角色。 如需有關安裝 Master Data Services 與建立 Master Data Services 資料庫的詳細資訊，請參閱＜ [Install Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)＞。  
  
6.  當安裝成功地完成之後，將會顯示完成訊息。 按任意鍵關閉命令提示字元視窗。  
  
##  <a name="CommandPrompt"></a> 從命令提示字元執行 DQSInstaller.exe  
 您可以在命令提示字元中使用下列命令列參數執行 DQSInstaller.exe：  
  
|DQSInstaller.exe 參數|描述|範例語法|  
|--------------------------------|-----------------|-------------------|  
|-collation|要用於安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]的伺服器定序。<br /><br /> DQS 僅支援不區分大小寫的定序。 如果您指定區分大小寫的定序，則安裝程式會嘗試使用所指定定序的不區分大小寫版本。 如果沒有不區分大小寫的版本，或是 SQL 不支援定序，則 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 安裝會失敗。<br /><br /> 如果未指定伺服器定序，則會使用預設定序 SQL_Latin1_General_CP1_CI_AS。|`dqsinstaller.exe –collation <collation_name>`|  
|-upgradedlls|略過重新建立 DQS 資料庫 (DQS_MAIN、DQS_PROJECTS 和 DQS_STAGING_DATA)，並且僅更新 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 資料庫中 DQS 所使用的 SQL Common Language Runtime (SQLCLR) 組件。<br /><br /> 如需詳細資訊，請參閱 [在 .NET Framework 更新之後升級 SQLCLR 組件](upgrade-sqlclr-assemblies-after-net-framework-update.md)。|`dqsinstaller.exe -upgradedlls`|  
|-exportkbs|將所有知識庫匯出到 DQS 備份檔 (.dqsb)。 您還必須指定要匯出所有知識庫的目標完整路徑和檔案名稱。<br /><br /> 如需詳細資訊，請參閱＜ [使用 DQSInstaller.exe 匯出及匯入 DQS 知識庫](export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)＞。|`dqsinstaller.exe –exportkbs <path><filename>`<br /><br /> 例如， `dqsinstaller.exe –exportkbs c:\DQSBackup.dqsb`|  
|-importkbs|完成 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 安裝後，從 DQS 備份檔 (.dqsb) 匯入所有知識庫。 您還必須指定要匯入所有知識庫的來源完整路徑和檔案名稱。<br /><br /> 如需詳細資訊，請參閱＜ [使用 DQSInstaller.exe 匯出及匯入 DQS 知識庫](export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)＞。|`dqsinstaller.exe –importkbs <path><filename>`<br /><br /> 例如， `dqsinstaller.exe –importkbs c:\DQSBackup.dqsb`|  
|-upgrade|升級 DQS 資料庫結構描述。 在先前設定的 DQS 執行個體上安裝 SQL Server 更新之後，您必須使用這個參數。 如需詳細資訊，請參閱＜ [Upgrade DQS Databases Schema After Installing SQL Server Update](upgrade-dqs-databases-schema-after-installing-sql-server-update.md)＞。|`dqsinstaller.exe -upgrade`|  
|-uninstall|從目前的 SQL Server 執行個體解除安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 。<br /><br /> 您也可以將現有資料品質伺服器安裝中的所有知識庫匯出到 DQS 備份檔，然後解除安裝資料品質伺服器。 如需詳細資訊，請參閱＜ [使用 DQSInstaller.exe 匯出及匯入 DQS 知識庫](export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)＞。<br /><br /> **\*\* 重要事項 \*\*** 如果使用 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 命令列參數解除安裝 SQL Server 執行個體上的 `–uninstall` ，則在解除安裝過程中將刪除所有 DQS 物件。 如 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 移除 Data Quality Server 物件 [中所述，您不必在解除安裝](../../sql-server/install/remove-data-quality-server-objects.md)之後手動刪除這些物件。|**若只要解除安裝資料品質伺服器：** <br /> `dqsinstaller.exe –uninstall`<br /><br /> **若要將所有知識庫匯出到檔案，然後解除安裝資料品質伺服器：** <br /> `dqsinstaller.exe –uninstall <path><filename>` <br />例如， `dqsinstaller.exe –uninstall c:\DQSBackup.dqsb`|  
  
 **若要從命令提示字元執行 DQSInstaller.exe：**  
  
1.  啟動 [命令提示字元]。  
  
2.  在命令提示字元中，將目錄變更為 DQSInstaller.exe 所在的位置。 如果已經安裝了 SQL Server 的預設執行個體，DQSInstaller.exe 檔會位於 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn。  
  
    ```  
    cd C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn  
    ```  
  
3.  在命令提示字元中，於使用或不使用命令列參數的情況下執行 DQSInstaller.exe：  
  
    -   **不使用命令列參數**：輸入 `dqsinstaller.exe`，然後按 ENTER。  
  
    -   **使用命令列參數**：輸入上表中所述的必要命令，然後按 ENTER。  
  
4.  必要的動作會依據指定的命令執行。 如果您剛剛選擇不使用任何命令列參數安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] ，則其餘步驟與上一節 [從開始畫面、開始功能表或 Windows 檔案總管執行 DQSInstaller.exe](run-dqsinstaller-exe-to-complete-data-quality-server-installation.md#WindowsExplorer)中步驟 2-6 所述相同。  
  
## <a name="next-steps"></a>後續步驟  
  
-   依據工作設定檔授與使用者適當的 DQS 角色。 請參閱 [對使用者授與 DQS 角色](grant-dqs-roles-to-users.md)。  
  
-   如果要從 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 遠端存取 [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]，請使用此電腦的 SQL Server 組態管理員啟用 TCP/IP 通訊協定。  
  
-   確認您可以存取 DQS 作業的來源資料，並且能夠將已處理的資料匯出到資料庫中的某個資料表。 請參閱 [存取用於 DQS 作業的資料](access-data-for-the-dqs-operations.md)。  
  
## <a name="see-also"></a>另請參閱  
 [安裝 Data Quality Services](install-data-quality-services.md)   
 [在 .NET Framework 更新之後升級 SQLCLR 組件](upgrade-sqlclr-assemblies-after-net-framework-update.md)   
 [使用 DQSInstaller.exe 匯出及匯入 DQS 知識庫](export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)  
  
  