---
title: 管理報表伺服器資料庫 (SSRS 原生模式) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], databases
- renaming databases
- report server database
- databases [Reporting Services], administering
- reportservertempdb
- reportserver database
ms.assetid: 97b2e1b5-3869-4766-97b9-9bf206b52262
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bc152d3130d903f4b098a495451d2918abcd7329
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59961134"
---
# <a name="administer-a-report-server-database-ssrs-native-mode"></a>管理報表伺服器資料庫 (SSRS 原生模式)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 部署會使用兩個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 關聯式資料庫供內部儲存之用。 根據預設，資料庫是命名為 ReportServer 和 ReportServerTempdb。 ReportServerTempdb 是由主要報表伺服器資料庫所建立，用於儲存暫存資料、工作階段資訊和快取報表。  
  
 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，資料庫管理工作包含備份與還原報表伺服器資料庫，以及管理用於將敏感性資料加密與解密的加密金鑰。  
  
 為了管理報表伺服器資料庫， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供許多工具。  
  
-   若要備份或還原報表伺服器資料庫、移動報表伺服器資料庫，或復原1表伺服器資料庫，您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令或資料庫命令提示字元公用程式。 如需指示，請參閱《SQL Server 線上叢書》中的[將報表伺服器資料庫移至其他電腦 &#40;SSRS 原生模式&#41;](moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)。  
  
-   若要將現有的資料庫內容複製到其他報表伺服器資料庫，您可以附加報表伺服器資料庫的複本，並將這個複本與不同的報表伺服器執行個體一起使用。 或者，您也可以建立並執行使用 SOAP 呼叫的指令碼，在新的資料庫中重新建立報表伺服器內容。 您可以使用 **rs** 公用程式執行指令碼。  
  
-   若要管理報表伺服器和報表伺服器資料庫之間的連接，以及找出特定報表伺服器執行個體所使用的資料庫，您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]組態工具中的 [資料庫安裝] 頁面。 若要深入了解報表伺服器資料庫的報表伺服器連接，請參閱 [設定報表伺服器資料庫連接 &#40;SSRS 組態管理員&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。  
  
## <a name="sql-server-login-and-database-permissions"></a>SQL Server 登入和資料庫的權限  
 報表伺服器資料庫可供報表伺服器在內部使用。 任何一個資料庫的連接都是由報表伺服器服務所建立的。 您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具來設定報表伺服器資料庫的報表伺服器連接。  
  
 資料庫之報表伺服器連接的認證可以是服務帳戶、Windows 本機或網域使用者帳戶，或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫使用者。 您必須針對連接選擇現有的帳戶。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不會自動為您建立帳戶。  
  
 系統會針對您指定的帳戶自動建立報表伺服器資料庫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
 此外，系統也會自動設定資料庫的權限。 Reporting Services 組態工具會將帳戶或資料庫使用者指派至報表伺服器資料庫的 `Public` 和 `RSExecRole` 角色。 `RSExecRole` 提供用來存取資料庫資料表及執行預存程序的權限。 `RSExecRole`當您建立報表伺服器資料庫時，會建立 master 和 msdb 中。 `RSExecRole` 是報表伺服器資料庫之 `db_owner` 角色的成員，可讓報表伺服器在支援自動升級程序的情況下更新自己的結構描述。  
  
## <a name="naming-conventions-for-the-report-server-databases"></a>報表伺服器資料庫的命名慣例  
 建立主要資料庫時，資料庫的名稱必須遵循為 [資料庫識別碼](../../relational-databases/databases/database-identifiers.md)指定的規則。 暫存資料庫名稱必須與主要報表伺服器資料庫的名稱相同，但要加上 Tempdb 後置詞。 您不能將暫存資料庫命名為不同的名稱。  
  
 不支援重新命名報表伺服器資料庫，因為報表伺服器資料庫是被視為內部元件， 如果重新命名報表伺服器資料庫將會發生錯誤。 特別是，如果重新命名主要資料庫，將會出現錯誤訊息，說明資料庫名稱未同步。如果您重新命名 ReportServerTempdb 資料庫，稍後執行報表時就會發生下列內部錯誤：  
  
 「報表伺服器發生內部錯誤。 請參閱錯誤記錄以取得更多詳細資料。 (rsInternalError)  
  
 無效的物件名稱 'ReportServerTempDB.dbo.PersistedStream'。」  
  
 發生這個錯誤是因為 ReportServerTempdb 名稱是儲存於內部，以供預存程序執行內部作業之用， 如果重新命名此暫存資料庫將會造成預存程序無法正常運作。  
  
## <a name="enabling-snapshot-isolation-on-the-report-server-database"></a>在報表伺服器資料庫上啟用快照集隔離  
 您無法在報表伺服器資料庫上啟用快照集隔離。 如果快照隔離已開啟，您將會遇到下列錯誤：「 選取的報表不是就緒可供檢視。 報表仍在轉譯中，或報表快照集無法使用」。  
  
 如果您並未刻意啟用快照集隔離，表示可能有另一個應用程式已經設定此屬性，或者 **model** 資料庫可能啟用了快照集隔離，因而導致所有新資料庫都繼承此設定。  
  
 若要在報表伺服器上關閉快照集隔離，請啟動 Management Studio、開啟新的查詢視窗、貼上下列指令碼，然後執行：  
  
```  
ALTER DATABASE ReportServer  
SET ALLOW_SNAPSHOT_ISOLATION OFF  
ALTER DATABASE ReportServerTempdb  
SET ALLOW_SNAPSHOT_ISOLATION OFF  
ALTER DATABASE ReportServer  
SET READ_COMMITTED_SNAPSHOT OFF  
ALTER DATABASE ReportServerTempDb  
SET READ_COMMITTED_SNAPSHOT OFF  
```  
  
## <a name="about-database-versions"></a>關於資料庫版本  
 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，沒有提供有關資料庫版本的明確資訊。 不過，因為資料庫版本一律與產品版本同步，所以您可以使用產品版本資訊，得知資料庫版本變更的時間。 產品版本資訊[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]表示透過檔案版本資訊出現在記錄檔中，所有的 SOAP 呼叫的標頭中，而且當您連接到報表伺服器 URL (例如，當您開啟瀏覽器並前往 http://localhost/reportserver)。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [建立原生模式報表伺服器資料庫 &#40;SSRS 組態管理員&#41;](../install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [設定報表伺服器服務帳戶 &#40;SSRS 組態管理員&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [設定報表伺服器資料庫連接 &#40;SSRS 組態管理員&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [建立報表伺服器資料庫 &#40;SSRS 組態管理員&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)   
 [Reporting Services 的備份與還原作業](../install-windows/backup-and-restore-operations-for-reporting-services.md)   
 [報表伺服器資料庫 &#40;SSRS 原生模式&#41;](report-server-database-ssrs-native-mode.md)   
 [Reporting Services 報表伺服器 &#40;原生模式&#41;](reporting-services-report-server-native-mode.md)   
 [儲存加密的報表伺服器資料 &#40;SSRS 組態管理員&#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [設定和管理加密金鑰 &#40;SSRS 組態管理員&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
