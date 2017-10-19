---
title: "重新命名管理 SQL Server 獨立執行個體的電腦 | Microsoft Docs"
ms.custom: 
ms.date: 09/08/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- remote login errors [SQL Server]
- standalone computer names [SQL Server]
- names [SQL Server], standalone instances of SQL Server
- renaming standalone instances of SQL Server
- sysservers system table
- removing remote logins
- deleting remote logins
- dropping remote logins
ms.assetid: bbaf1445-b8a2-4ebf-babe-17d8cf20b037
caps.latest.revision: 31
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1df54edd5857ac2816fa4b164d268835d9713638
ms.openlocfilehash: 3409cf7906f37569763ac2277ea82fe1d0fe4c82
ms.contentlocale: zh-tw
ms.lasthandoff: 09/12/2017

---
# <a name="rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server"></a>重新命名主控 SQL Server 獨立式執行個體的電腦
當您變更了執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的電腦名稱之後，便會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動期間辨識這個新名稱。 您不必重新執行安裝程式，即可重設電腦名稱。 請改用下列步驟來更新儲存在 sys.servers 中而且由系統函式 @@SERVERNAME 所報告的系統中繼資料。 您可以更新系統中繼資料，以便反映使用 @@SERVERNAME 或從 sys.servers 中查詢伺服器名稱之遠端連接和應用程式的電腦名稱變更。  
  
您不能使用下列步驟重新命名 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。 這些步驟只能用來重新命名執行個體名稱中與電腦名稱相對應的部分。 例如，您可以將主控 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體 (名為 Instance1) 的電腦名稱 MB1 改成其他名稱，例如 MB2。 不過，該名稱中的執行個體部分 Instance1 將保持不變。 在這個範例中， \\\\*ComputerName*\\*InstanceName* 會從 \\\MB1\Instance1 變更為 \\\MB2\Instance1。  
  
 **開始之前**  
  
 在開始執行重新命名程序之前，請先檢閱下列資訊：  
  
-   當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集的一部分時，此電腦的重新命名程序與主控獨立執行個體的電腦程序不同。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援在複寫時重新命名電腦，但在複寫時使用記錄傳送的情況例外。 如果主要電腦已永久遺失，可以重新命名記錄傳送的次要電腦。 如需詳細資訊，請參閱[記錄傳送和複寫 &#40;SQL Server&#41;](../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md)。  
  
-   當您要重新命名設定為使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的電腦時，[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 在電腦名稱變更之後可能無法使用。 如需詳細資訊，請參閱 [重新命名報表伺服器電腦](../../reporting-services/report-server/rename-a-report-server-computer.md)。  
  
-   當您要重新命名已設定為使用資料庫鏡像的電腦時，您必須在重新命名作業之前關閉資料庫鏡像。 然後使用新的電腦名稱，重新建立資料庫鏡像。 資料庫鏡像的中繼資料並不會自動更新來反映新的電腦名稱。 請使用下列步驟來更新系統中繼資料。  
  
-   透過以硬式編碼方式參考電腦名稱的 Windows 群組來連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的使用者，可能無法連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果 Windows 群組指定舊的電腦名稱，則重新命名之後可能會發生這個狀況。 為了確保這種 Windows 群組在重新命名作業之後仍能連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請更新 Windows 群組，以指定新的電腦名稱。  
  
 重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之後，您可以使用新的電腦名稱連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 為了確定 @@SERVERNAME 傳回已更新的本機伺服器執行個體名稱，您應該手動執行下列適用於您狀況的程序。 您所使用的程序需視正在更新的電腦是主控 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]預設執行個體還是具名執行個體而定。  
  
## <a name="rename-a-computer-that-hosts-a-stand-alone-instance-of-includessnoversionincludesssnoversion-mdmd"></a>重新命名裝載 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 獨立執行個體的電腦  
  
-   若為主控 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]預設執行個體的重新命名電腦，請執行下列程序：  
  
    ```sql
    sp_dropserver <old_name>;  
    GO  
    sp_addserver <new_name>, local;  
    GO  
    ```  
  
     重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。  
  
-   若為主控 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]具名執行個體的重新命名電腦，請執行下列程序：  
  
    ```sql
    sp_dropserver <old_name\instancename>;  
    GO  
    sp_addserver <new_name\instancename>, local;  
    GO  
    ```  
  
     重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。  
  
## <a name="after-the-renaming-operation"></a>在重新命名作業之後  
 在重新命名電腦之後，使用舊電腦名稱的任何連接都必須使用新名稱來連接。  
  
## <a name="verify-renaming-operation"></a>確認重新命名作業  
  
-   從 @@SERVERNAME 或 sys.servers 中選取資訊。 @@SERVERNAME 函式會傳回新名稱，而且 sys.servers 資料表會顯示新名稱。 下列範例示範如何使用 @@SERVERNAME。   
  
    ```  
    SELECT @@SERVERNAME AS 'Server Name';  
    ```  
  
## <a name="additional-considerations"></a>其他考量  
 **遠端登入** - 如果電腦上已有遠端登入，則執行 **sp_dropserver** 可能會產生類似下面的錯誤：  
  
 `Server: Msg 15190, Level 16, State 1, Procedure sp_dropserver, Line 44 There are still remote logins for the server 'SERVER1'.`  
  
 若要解決錯誤，您必須卸除這部伺服器的遠端登入。  
  
### <a name="drop-remote-logins"></a>卸除遠端登入  
  
-   如果是預設執行個體，請執行下列程序：  
  
    ```sql
    sp_dropremotelogin old_name;  
    GO  
    ```  
  
-   如果是具名執行個體，請執行下列程序：  
  
    ```sql
    sp_dropremotelogin old_name\instancename;  
    GO  
    ```  
  
 **連結的伺服器組態** - 連結的伺服器組態將會受到電腦重新命名作業影響。 您可以使用 **sp_addlinkedserver** 或 **sp_setnetname** 更新電腦名稱參考。 如需詳細資訊，請參閱 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 或 [sp_setnetname &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setnetname-transact-sql.md)。  
  
 **用戶端別名名稱** - 使用具名管道的用戶端別名將會受到電腦重新命名作業影響。 例如，如果您建立了指向 SRVR1 的別名 "PROD_SRVR" 並且使用具名管道通訊協定，此管道名稱將會類似這樣： `\\SRVR1\pipe\sql\query`。 重新命名電腦之後，具名管道的路徑將不再有效。 如需具名管道的詳細資訊，請參閱 [使用具名管道建立有效的連接字串](http://go.microsoft.com/fwlink/?LinkId=111063)。  
  
## <a name="see-also"></a>另請參閱  
 [安裝 SQL Server](../../database-engine/install-windows/install-sql-server.md)  
  
  
