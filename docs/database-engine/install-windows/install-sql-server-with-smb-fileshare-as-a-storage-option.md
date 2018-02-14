---
title: "安裝 SQL Server 與 SMB 檔案共用儲存體 | Microsoft Docs"
ms.custom: 
ms.date: 09/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8b7810b2-637e-46a3-9fe1-d055898ba639
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3b1f88c6df9ea20d8fb0b2b27dbd5e40d6c6dfa7
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="install-sql-server-with-smb-fileshare-storage"></a>安裝 SQL Server 與 SMB 檔案共用儲存體

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]開始，系統資料庫 (Master、Model、MSDB 和 TempDB) 與 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 使用者資料庫可以當作儲存選項與伺服器訊息區塊 (SMB) 檔案伺服器一起安裝。 這同時適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 獨立安裝和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集安裝 (FCI)。  
  
> [!NOTE]  
>  SMB 檔案共用目前不支援檔案資料流。  
  
## <a name="installation-considerations"></a>安裝考量  
  
### <a name="smb-fileshare-formats"></a>SMB 檔案共用格式：  
 指定 SMB 檔案共用時，支援獨立和 FCI 資料庫的通用命名慣例 (UNC) 路徑格式如下：  
  
-   \\\ServerName\ShareName\  
  
-   \\\ServerName\ShareName  
  
 如需通用命名慣例的詳細資訊，請參閱 [UNC](http://msdn.microsoft.com/library/gg465305.aspx)。  
  
 不建議使用回送 UNC 路徑 (伺服器名稱為 localhost (127.0.0.1) 的 UNC 路徑，或是本機電腦名稱)。 使用檔案伺服器叢集的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (裝載於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行的相同節點上) 也不受支援，這是特殊案例。 為了避免這個狀況發生，建議將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和檔案伺服器叢集建立在不同的 Windows 叢集上。  
  
 底下的 UNC 路徑格式不受支援：  
  
-   迴路路徑，例如 \\\localhost\\..\ 或 \\\127.0.0.1\\...\  
  
-   管理共用，例如 \\\servername\x$  
  
-   其他 UNC 路徑格式，例如 \\\\?\x:\  
  
-   對應的網路磁碟機。  
  
### <a name="supported-data-definition-language-ddl-statements"></a>支援的資料定義語言 (DDL) 陳述式  
 以下的 [!INCLUDE[tsql](../../includes/tsql-md.md)] DDL 陳述式和 Database Engine 預存程序支援 SMB 檔案共用：  
  
1.  [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
2.  [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
3.  [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
4.  [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)  
  
### <a name="installation-options"></a>安裝選項  
  
-   在安裝程式 UI [資料庫引擎組態] 頁面的 [資料目錄] 索引標籤中，將「資料根目錄」參數設定為 “\\\fileserver1\share1\”。  
  
-   在命令提示字元安裝中，將 “/INSTALLSQLDATADIR” 指定為 “\\\fileserver1\share1\”。  
  
     以下是使用 SMB 檔案共用選項在獨立伺服器上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的範例語法：  
  
    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="<StrongPassword>" /INSTALLSQLDATADIR="\\FileServer\Share1\" /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
     安裝具有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 等預設執行個體的單一節點 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]容錯移轉叢集執行個體：  
  
    ```  
    setup.exe /q /ACTION=InstallFailoverCluster /InstanceName=MSSQLSERVER /INDICATEPROGRESS /ASSYSADMINACCOUNTS="<DomainName\UserName>" /ASDATADIR=<Drive>:\OLAP\Data /ASLOGDIR=<Drive>:\OLAP\Log /ASBACKUPDIR=<Drive>:\OLAP\Backup /ASCONFIGDIR=<Drive>:\OLAP\Config /ASTEMPDIR=<Drive>:\OLAP\Temp /FAILOVERCLUSTERDISKS="<Cluster Disk Resource Name - for example, 'Disk S:'" /FAILOVERCLUSTERNETWORKNAME="<Insert Network Name>" /FAILOVERCLUSTERIPADDRESSES="IPv4;xx.xxx.xx.xx;Cluster Network;xxx.xxx.xxx.x" /FAILOVERCLUSTERGROUP="MSSQLSERVER" /Features=AS,SQL /ASSVCACCOUNT="<DomainName\UserName>" /ASSVCPASSWORD="xxxxxxxxxxx" /AGTSVCACCOUNT="<DomainName\UserName>" /AGTSVCPASSWORD="xxxxxxxxxxx" /INSTALLSQLDATADIR="\\FileServer\Share1\" /SQLCOLLATION="SQL_Latin1_General_CP1_CS_AS" /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="xxxxxxxxxxx" /SQLSYSADMINACCOUNTS="<DomainName\UserName> /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
     如需在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中使用各種命令列參數選項的詳細資訊，請參閱 [從命令提示字元安裝 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)。  
  
## <a name="operating-system-considerations-smb-protocol-vs-includessnoversionincludesssnoversion-mdmd"></a>作業系統考量 (SMB 通訊協定與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])  
 不同的 Windows 作業系統有不同的 SMB 通訊協定版本，而且 SMB 通訊協定版本對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]而言是透明的。 您可以找到不同 SMB 通訊協定版本相對於 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的優點。  
  
|作業系統|SMB2 通訊協定版本|對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|----------------------|---------------------------|-------------------------------------------|  
|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP 2|2.0|相較於舊版 SMB，新版中已改良效能。<br /><br /> 持久性，有助於從暫時性網路問題復原。|  
|[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP 1，包括 Server Core|2.1|支援大型 MTU，有助於大型資料傳送，例如 SQL 備份和還原。 此功能必須由使用者啟用。 如需如何啟用此功能的詳細資料，請參閱 [SMB 的新功能](http://go.microsoft.com/fwlink/?LinkID=237319) (http://go.microsoft.com/fwlink/?LinkID=237319)。<br /><br /> 大幅改良效能，特別是針對 SQL OLTP 樣式工作負載方面。 這些效能改良需要套用 Hotfix。 如需 Hotfix 的詳細資訊，請參閱 [此網頁](http://go.microsoft.com/fwlink/?LinkId=237320) (http://go.microsoft.com/fwlink/?LinkId=237320)。|  
|[!INCLUDE[win8srv](../../includes/win8srv-md.md)]，包括 Server Core|3.0|支援以透明方式容錯移轉檔案共用，不需任何停機時間，而且系統管理員也不需要介入檔案伺服器叢集組態的 SQL DBA 或檔案伺服器管理員。<br /><br /> 支援同時使用多網路介面的 IO，並容忍網路介面失敗。<br /><br /> 支援具有 RDMA 功能的網路介面。<br /><br /> 如需這些功能和伺服器訊息區塊的詳細資訊，請參閱 [伺服器訊息區塊概觀](http://go.microsoft.com/fwlink/?LinkId=253174) (http://go.microsoft.com/fwlink/?LinkId=253174)。<br /><br /> 支援向外延展檔案伺服器 (SoFS) 的持續可用性。|  
|[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2，包括 Server Core|3.2|支援以透明方式容錯移轉檔案共用，不需任何停機時間，而且系統管理員也不需要介入檔案伺服器叢集組態的 SQL DBA 或檔案伺服器管理員。<br /><br /> 利用 SMB Multichannel，支援同時使用多網路介面的 IO，並容忍網路介面失敗。<br /><br /> 利用 SMB Direct 支援具有 RDMA 功能的網路介面。<br /><br /> 如需這些功能和伺服器訊息區塊的詳細資訊，請參閱 [伺服器訊息區塊概觀](http://go.microsoft.com/fwlink/?LinkId=253174) (http://go.microsoft.com/fwlink/?LinkId=253174)。<br /><br /> 支援向外延展檔案伺服器 (SoFS) 的持續可用性。<br /><br /> 最佳化對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLTP 的常用小型隨機讀取/寫入 I/O。<br /><br /> 預設會啟動最大傳輸單位 (MTU)，可大幅提高大型循序傳送的效能，例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料倉儲及資料庫備份或還原。|  
  
## <a name="security-considerations"></a>安全性考量  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶應該擁有 SMB 共用資料夾的 FULL CONTROL 共用權限及 NTFS 權限。 如果使用 SMB 檔案伺服器， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶可以是網域帳戶或系統帳戶。 如需共用和 NTFS 權限的詳細資訊，請參閱 [檔案伺服器的共用及 NTSF 權限](http://go.microsoft.com/fwlink/?LinkId=245535) (http://go.microsoft.com/fwlink/?LinkId=245535)。  
  
    > [!NOTE]  
    >  SMB 共用資料夾的 FULL CONTROL 共用權限及 NTFS 權限僅限於： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶以及具有管理伺服器角色的 Windows 使用者。  
  
     建議使用網域帳戶當做 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶。 如果將系統帳戶當作服務帳戶使用，請以下列格式授與電腦帳戶的權限：\<<網域名稱>>\\<電腦名稱><>\*$*。  
  
    > [!NOTE]  
    >  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間，如果將 SMB 檔案共用指定為儲存選項，則必須將網域帳戶指定為服務帳戶。 在 SMB 檔案共用中，系統帳戶只能指定為服務帳戶後續 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝。  
    >   
    >  虛擬帳戶無法對遠端位置驗證。 所有虛擬帳戶都使用電腦帳戶的權限。 使用下列格式佈建電腦帳戶：\<<網域名稱>>\\<<電腦名稱>>\*$*。  
  
-   在叢集安裝期間，用來安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的帳戶應該擁有當做資料目錄使用之 SMB 檔案共用資料夾，或是其他任何資料夾 (使用者資料庫目錄、使用者資料庫記錄檔目錄、TempDB 目錄、TempDB 記錄檔目錄、備份目錄) 的 FULL CONTROL 權限。  
  
-   用於安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的帳戶應該具有 SMB 檔案伺服器的 SeSecurityPrivilege 權限。 若要授與此權限，請使用檔案伺服器上的 [本機安全性原則] 主控台，將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式帳戶新增至 [管理稽核和安全性記錄檔] 原則中。 在 [本機安全性原則] 主控台中 [本機原則] 下的 [使用者權利指派] 區段可以找到此設定。  
  
## <a name="known-issues"></a>已知問題  
  
-   在您卸離位於連接網路之儲存裝置上的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 資料庫之後，當您嘗試重新附加 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫時，可能會遇到資料庫權限問題。 [此知識庫文章](http://go.microsoft.com/fwlink/?LinkId=237321) (http://go.microsoft.com/fwlink/?LinkId=237321) 中有定義這個問題。 若要暫時解決此問題，請參閱此知識庫文件中的＜ **其他相關資訊** ＞。  
  
-   如果 SMB 檔案共用當做 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]叢集執行個體的儲存選項使用，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集診斷記錄預設將無法寫入檔案共用，因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源 DLL 缺少此檔案共用的讀取/寫入權限。 若要解決這個問題，請嘗試下列其中一個方法：  
  
    1.  授與檔案共用的讀取/寫入權限給叢集中的所有電腦物件。  
  
    2.  將診斷記錄的位置設定為本機檔案路徑。 請參閱下列範例：  
  
        ```sql  
        ALTER SERVER CONFIGURATION  
        SET DIAGNOSTICS LOG PATH = 'C:\logs';  
        ```  
  
## <a name="see-also"></a>另請參閱  
 [規劃 SQL Server 安裝](../../sql-server/install/planning-a-sql-server-installation.md)   
 [設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  
