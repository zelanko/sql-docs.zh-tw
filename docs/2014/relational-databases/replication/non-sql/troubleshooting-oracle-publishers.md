---
title: 針對 Oracle 發行者進行疑難排解 | Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], troubleshooting
- troubleshooting [SQL Server replication], Oracle publishing
ms.assetid: be94f1c1-816b-4b1d-83f6-2fd6f5807ab7
caps.latest.revision: 60
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: eb111251bfd3ae71e471a84a444c21acd091b449
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036334"
---
# <a name="troubleshooting-oracle-publishers"></a>Oracle 發行者疑難排解
  本主題列出設定和使用「Oracle 發行者」時可能發生的一些問題。  
  
## <a name="an-error-is-raised-regarding-oracle-client-and-networking-software"></a>發生有關 Oracle 用戶端與網路軟體的錯誤  
 在「散發者」執行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的帳戶必須對 Oracle 用戶端網路軟體的安裝目錄 (以及所有子目錄) 具有讀取與執行權限。 如果沒有被授與權限或者 Oracle 用戶端元件沒有正確安裝，您將收到下列錯誤訊息：  
  
 「由於 [Microsoft OLE DB Provider for Oracle]，連接到伺服器失敗。 找不到 Oracle 用戶端和網路元件。 這些元件由 Oracle 公司提供，是 Oracle 7.3.3 或更新版本用戶端軟體安裝的一部分。 在這些元件安裝前，Provider 無法運作」。  
  
 如果在「散發者」端已安裝適當的 Oracle 用戶端，請確定在用戶端完成安裝後，停止並重新啟動 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 為了讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 辨識用戶端元件，這是必要的動作。  
  
 如果您確認已被授與權限並且元件已安裝正確，但仍產生此錯誤，請確認 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDTC\MTxOCI 的登錄設定正確：  
  
-   對於 Oracle 10g，正確的設定為  
  
    -   OracleOciLib = oci.dll  
  
    -   OracleSqlLib = orasql10.dll  
  
    -   OracleXaLib = oraclient10.dll  
  
-   對於 Oracle 9i，正確的設定為  
  
    -   OracleOciLib = oci.dll  
  
    -   OracleSqlLib = orasql9.dll  
  
    -   OracleXaLib = oraclient9.dll  
  
## <a name="the-sql-server-distributor-cannot-connect-to-the-oracle-database-instance"></a>SQL Server 散發者無法連接到 Oracle 資料庫執行個體  
 如果「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」無法連接到「Oracle 發行者」，請確定：  
  
-   「散發者」上安裝了必要的 Oracle 軟體。  
  
-   Oracle 資料庫在線上，並且您可以使用 SQL*Plus 之類的工具與其連接。  
  
-   複寫用於連接到「Oracle 發行者」的登入擁有足夠權限。 如需詳細資訊，請參閱[設定 Oracle 發行者](configure-an-oracle-publisher.md)。  
  
-   在「Oracle 發行者」設定期間定義的 TNS 名稱列在 tnsnames.ora 檔案中。  
  
-   使用正確的 Oracle 首頁和路徑。 即使「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」上只安裝一組 Oracle 二進位編碼檔案，也請確定正確設定了與 Oracle 首頁相關的環境變數。 如果變更環境變數值，必須停止並重新啟動 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，才能使變更生效。  
  
 如需設定和測試連接的詳細資訊，請參閱[設定 Oracle 發行者](configure-an-oracle-publisher.md)中的＜在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者上安裝與設定 Oracle 用戶端網路軟體＞。  
  
## <a name="the-oracle-publisher-is-associated-with-another-distributor"></a>Oracle 發行者與另一散發者產生關聯  
 一個「Oracle 發行者」只能與一個「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」相關聯。 如果有另一個「散發者」與該「Oracle 發行者」相關聯，則必須在卸除它之後方可使用另一個「散發者」。 如果沒有先卸除該「散發者」，您將收到下列錯誤訊息之一：  
  
-   「Oracle 伺服器執行個體 '\<Oracle 發行者名稱>' 之前已經設定使用 '\<SQL Server 散發者名稱>' 作為其散發者。 若要開始使用 '\<新的 SQL Server 散發者名稱>' 作為其散發者，您必須移除 Oracle 伺服器執行個體上目前的複寫組態，這會刪除該伺服器執行個體上的所有發行集」。  
  
-   「Oracle 伺服器 '\<Oracle 伺服器名稱>' 已經在散發者 '\<SQL Server 散發者名稱>.\<散發資料庫名稱>' 上定義為發行者 '\<Oracle 發行者名稱>'。 請卸除發行者或是卸除公用同義字 '\<同義字名稱>' 來重新建立」。  
  
 在卸除某個「Oracle 散發者」時，Oracle 資料庫中的複寫物件也會自動清除。 但是在某些情況下必須手動清除 Oracle 複寫物件。 若要手動清除複寫建立的 Oracle 複寫物件：  
  
1.  連接到具有 DBA 權限的 Oracle 發行者。  
  
2.  發出 SQL 命令 `DROP PUBLIC SYNONYM MSSQLSERVERDISTRIBUTOR;`。  
  
3.  發出 SQL 命令 `DROP USER <replication_administrative_user_schema>``CASCADE;`。  
  
## <a name="sql-server-error-21663-is-raised-regarding-the-lack-of-a-primary-key"></a>發生有關缺少主索引鍵的 SQL Server 錯誤 21663  
 交易式發行集中的發行項必須擁有有效的主索引鍵。 如果它們沒有有效的主索引鍵，您將在嘗試新增發行項時收到下列錯誤訊息：  
  
 「找不到有效的來源資料表 [\<資料表擁有者>].[\<資料表名稱>] 主索引鍵。」  
  
 如需主索引鍵需求的詳細資訊，請參閱＜ [Design Considerations and Limitations for Oracle Publishers](design-considerations-and-limitations-for-oracle-publishers.md)＞主題中的＜唯一索引和條件約束＞一節。  
  
## <a name="sql-server-error-21642-is-raised-regarding-a-duplicate-linked-server-login"></a>發生有關重複連結伺服器登入的 SQL Server 錯誤 21642  
 在最初設定「Oracle 發行者」時，會為「發行者」與「散發者」之間的連接建立一個連結伺服器項目。 連結伺服器的名稱與 Oracle TNS 服務名稱相同。 如果您嘗試建立相同名稱的連結伺服器，將顯示下列錯誤訊息：  
  
 「異質性發行者需要已連結伺服器。 已經存在名稱為 '\<連結伺服器名稱>' 的連結伺服器。 請移除已連結伺服器或選擇不同的發行者名稱」。  
  
 如果您嘗試直接建立連結伺服器，或者您之前已卸除「Oracle 發行者」與「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」之間的關聯性，現在又嘗試重新設定，便可能引發此錯誤。 若在嘗試重新設定「發行者」時收到此錯誤，請使用 [sp_dropserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropserver-transact-sql) 卸除連結伺服器。  
  
 若您必須透過連結伺服器連線來連接到 Oracle 發行者，請建立另一個 TNS 服務名稱，然後在呼叫 [sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql) 時使用這個名稱。 如需建立 TNS 服務名稱的詳細資訊，請參閱 Oracle 文件集。  
  
## <a name="sql-server-error-21617-is-raised"></a>發生 SQL Server 錯誤 21617  
 Oracle 發行使用 Oracle 應用程式 SQL*PLUS 將「發行者」支援程式碼的封裝下載到 Oracle 資料庫。 嘗試設定 Oracle 發行者之前，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會確認是否可透過散發者上的系統路徑存取 SQL\*PLUS。 若無法載入 SQL\*PLUS，則會顯示下列錯誤訊息：  
  
 「無法執行 SQL*PLUS。 請確認散發者端已安裝目前版本的 Oracle 用戶端程式碼」。  
  
 嘗試在散發者上尋找 SQL\*PLUS。 對於 Oracle 10g 用戶端安裝，此可執行檔的名稱為 sqlplus.exe， 通常安裝於 %ORACLE_HOME%/bin。 若要確認 SQL\*PLUS 的路徑是否顯示在系統路徑中，請檢查系統變數 **Path** 的值：  
  
1.  以滑鼠右鍵按一下 **[我的電腦]**，然後再按 **[內容]**。  
  
2.  按一下 **[進階]** 索引標籤，然後再按 **[環境變數]**。  
  
3.  在 **[環境變數]** 對話方塊的 **[系統變數]** 清單中，選取 **[Path]** 變數，然後按一下 **[編輯]**。  
  
4.  在 **[編輯系統變數]** 對話方塊中：如果 **[變數值]** 文字方塊中不存在包含 sqlplus.exe 的資料夾路徑，則編輯字串以包含它。  
  
5.  按一下每個開啟對話方塊上的 **[確定]** ，以結束並儲存變更。  
  
 如果您在「散發者」上找不到 sqlplus.exe，請於「散發者」端安裝目前版本的 Oracle 用戶端軟體。 如需詳細資訊，請參閱[設定 Oracle 發行者](configure-an-oracle-publisher.md)。  
  
## <a name="sql-server-error-21620-is-raised"></a>發生 SQL Server 錯誤 21620  
 如果連接到 8.1 版之前的 Oracle 資料庫，Oracle 發行需要在散發者上安裝 9 版以上的 Oracle 用戶端軟體。 如果連接到 8.1 版或更新版本的 Oracle 資料庫，則建議採用 10 版或更新版本的 Oracle 用戶端軟體。  
  
 嘗試設定「Oracle 發行者」之前，Oracle 發行會確認可透過「散發者」上系統路徑存取的 SQL*PLUS 版本是不是 9 版或更新版本。 如果不是，會顯示下列錯誤訊息：  
  
 「可透過系統 Path 變數存取的 SQL*PLUS 版本，目前不足以支援 Oracle 發行。 請確認散發者端已安裝目前版本的 Oracle 用戶端程式碼」。  
  
 如果在「散發者」上安裝了多個版本的 Oracle 用戶端軟體，請確定最新版本至少是 9 版，並且系統 path 變數會首先參考此版本 (只要最新的版本最先出現，就會發生對其他版本的參考)。 如需有關編輯系統 path 變數的詳細資訊，請參閱本主題前面的＜發生 SQL Server 錯誤 21617＞一節。  
  
## <a name="sql-server-error-21624-or-error-21629-is-raised"></a>發生 SQL Server 錯誤 21624 或錯誤 21629  
 對於 64 位元的「散發者」，Oracle 發行會使用 Oracle OLEDB Provider for Oracle (OraOLEDB.Oracle)。 請確定已安裝 Oracle OLEDB 提供者，並在「散發者」上註冊。 如果未安裝和註冊提供者，便會顯示以下一或兩則錯誤訊息：  
  
-   在散發者 '%s' 端找不到已註冊的 Oracle OLEDB 提供者 (OraOLEDB.Oracle)。 請確認已安裝目前版本的 Oracle OLEDB 提供者，並在散發者端註冊」。  
  
-   「CLSID 登錄機碼指出散發者端沒有已經註冊的 Oracle OLEDB Provider for Oracle (OraOLEDB.Oracle)。 請確認已安裝 Oracle OLEDB 提供者，並在散發者端註冊」。  
  
 如果使用的是 10g 版的 Oracle 用戶端軟體，提供者為 OraOLEDB10.dll；如果是 9i 版，則提供者為 OraOLEDB.dll。 提供者安裝於 %ORACLE_HOME%\BIN (例如，C:\oracle\product\10.1.0\Client_1\bin)。 如果判斷出「散發者」端未安裝 Oracle OLEDB 提供者，請從 Oracle 提供的 Oracle 用戶端軟體安裝光碟片安裝它。 如需詳細資訊，請參閱[設定 Oracle 發行者](configure-an-oracle-publisher.md)。  
  
 如果安裝了 Oracle OLEDB 提供者，請確定其已註冊。 若要註冊提供者 DLL，請從安裝 DLL 的目錄執行下列命令，然後停止 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體，然後重新啟動它。  
  
1.  `regsvr32 OraOLEDB10.dll` 或 `regsvr32 OraOLEDB.dll`。  
  
## <a name="sql-server-error-21626-or-error-21627-is-raised"></a>發生 SQL Server 錯誤 21626 或錯誤 21627  
 為了確認 Oracle 發行環境是否設定正確， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會嘗試使用您在設定期間指定的登入認證連接「Oracle 發行者」。 如果「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」無法連接到「Oracle 發行者」，會顯示下列錯誤訊息：  
  
-   「無法使用 Oracle OLEDB 提供者 (OraOLEDB.Oracle) 連接到 Oracle 資料庫伺服器 '%s'。」  
  
 如果顯示此錯誤訊息，請透過使用「Oracle 發行者」設定期間指定的登入和密碼直接執行 SQL*PLUS，確認與 Oracle 資料庫的連接。 如需詳細資訊，請參閱本主題稍早的「SQL Server 散發者無法連接到 Oracle 資料庫執行個體」一節。  
  
## <a name="sql-server-error-21628-is-raised"></a>發生 SQL Server 錯誤 21628  
 對於 64 位元的「散發者」，Oracle 發行會使用 Oracle OLEDB Provider for Oracle (OraOLEDB.Oracle)。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會建立登錄項目，以允許使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]在處理序中執行 Oracle 提供者。 如果讀取或寫入此登錄項目時發生問題，則會顯示下列錯誤訊息：  
  
 「無法更新散發者 '%s' 的登錄，以允許使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]在處理序中執行 Oracle OLEDB 提供者 (OraOLEDB.Oracle)。 請確認目前的登入已獲得授權，可修改 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 擁有的登錄機碼」。  
  
 Oracle 發行需要存在登錄項目，且對於 64 位元「散發者」該登錄項目應設定為 **1** 。 如果該項目不存在， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會嘗試建立它。 如果該項目存在，但設定為 **0**，則設定不會變更；「Oracle 發行者」的設定將失敗。  
  
 若要檢視和修改登錄設定：  
  
1.  按一下 **[開始]**，然後按一下 **[執行]**。  
  
2.  在 **[執行]** 對話方塊中，輸入 **regedit**，然後按一下 **[確定]**。  
  
3.  巡覽至 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\\<執行個體名稱>\Providers。  
  
     [Providers] 下應包含一個名為 OraOLEDB.Oracle 的資料夾。 在此資料夾中應是 DWORD 值名稱 **AllowInProcess**，其值為 **1**。  
  
4.  如果判斷出 **AllowInProcess** 設定為 **0**，請將登錄項目更新為 **1**：  
  
    1.  以滑鼠右鍵按一下項目，然後再按 **[修改]**。  
  
    2.  在 **[編輯字串]** 對話方塊的 **[值資料]** 欄位中輸入 **[1]** 。  
  
## <a name="sql-server-error-21684-is-raised"></a>發生 SQL Server 錯誤 21684  
 如果管理的使用者帳戶沒有足夠權限，就會顯示下列錯誤訊息：  
  
 「與 Oracle 發行者 '%s' 管理者登入相關聯的權限不足。」  
  
 若要確認已授與使用者的權限，請執行下列查詢： `SELECT * from session_privs`。 輸出應如下所示：  
  
 `PRIVILEGE`  
  
 `------------------`  
  
 `CREATE SESSION`  
  
 `CREATE TABLE`  
  
 `CREATE PUBLIC SYNONYM`  
  
 `DROP PUBLIC SYNONYM`  
  
 `CREATE VIEW`  
  
 `CREATE SEQUENCE`  
  
 `CREATE PROCEDURE`  
  
 `CREATE TRIGGER`  
  
## <a name="you-encounter-permissions-issues-for-the-replication-user-schema"></a>遇到複寫使用者結構描述的權限問題  
 複寫使用者結構描述必須擁有[設定 Oracle 發行者](configure-an-oracle-publisher.md)的＜手動建立使用者結構描述＞中所述的權限。  
  
## <a name="oracle-error-ora-01000"></a>Oracle 錯誤 ORA-01000  
 將發行項新增至發行集的過程中，複寫使用「Oracle 發行者」的資料指標。 在此處理過程中，可能會超過「發行者」上可用資料指標的最大數目。 如果發生此種情形，則會產生下列錯誤：  
  
 「ORA-01000：超出開啟之資料指標的最大數目」  
  
 為避免此問題，請確定 Oracle 資料庫中的 **max_open_cursors** 設定已設成足夠大 (至少 1000)。 如需此設定的詳細資訊，請參閱 Oracle 文件集。  
  
## <a name="oracle-error-ora-01555"></a>Oracle 錯誤 ORA-01555  
 下列 Oracle 資料庫錯誤與快照式複寫無關；而與 Oracle 如何建構資料的讀取一致檢視相關：  
  
 「ORA-01555：快照集太舊」  
  
 Oracle 會在發出 SQL 陳述式時，使用稱為回復區段的物件建構資料的讀取一致檢視。 在回復資訊為其他並行的階段作業所覆寫時，可能會發生「快照集太舊」錯誤。 對於 Oracle 9i 之前的版本，建議使用以下方法來減少此錯誤的發生頻率：增加回復區段的大小和 (或) 數目，並將大型交易指派到特定的回復區段。  
  
 在 Oracle 9i 中，Oracle 提出了 UNDO 資料表空間概念來取代回復區段。 為防止在 Oracle 9i 中發生「快照集太舊」錯誤，建議您：  
  
-   建立一個包含適當可用空間量的 UNDO 資料表空間。  
  
-   在資料表空間上設定保留保證 (Oracle 10G 和更高版本)。  
  
-   設定 Oracle 初始化參數 UNDO_MANAGEMENT 與 UNDO_RETENTION。  
  
 如需避免「快照集太舊」錯誤的詳細資料，請參閱 Oracle 文件集。  
  
## <a name="oracle-error-ora-22285"></a>Oracle 錯誤 ORA-22285  
 如果資料表包括 BFILE 資料行，則該資料行的資料儲存在檔案系統中。 複寫管理使用者帳戶必須被授與目錄存取權限。在該目錄中，資料使用下列語法儲存：  
  
 `GRANT READ ON DIRECTORY <directory_name> TO <replication_administrative_user_schema>`  
  
 如果未授與存取權，「記錄讀取器代理程式」將發生下列錯誤：  
  
 「ORA-22285：目錄或 FILEOPEN 作業的檔案不存在」  
  
## <a name="changes-are-made-that-require-reconfiguration-of-the-publisher"></a>進行需要重新設定發行者的變更  
 對複寫中繼資料資料表或程序的變更要求您卸除「發行者」，然後對其重新設定。 若要重新設定「發行者」，必須先卸除「發行者」，然後再使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、Transact-SQL 或 RMO 重新設定。 如需設定發行者的詳細資訊，請參閱[設定 Oracle 發行者](configure-an-oracle-publisher.md)。  
  
 **卸除 Oracle 發行者 (** SQL Server Management Studio **)**  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 中「Oracle 發行者」的「散發者」，然後展開伺服器節點。  
  
2.  以滑鼠右鍵按一下 **[複寫]**，然後按一下 **[散發者屬性]**。  
  
3.  在 **[散發者屬性]** 對話方塊的 **[發行者]** 頁面上，清除「Oracle 發行者」的核取方塊。  
  
4.  按一下 [確定] 。  
  
 **若要卸除 Oracle 發行者 (Transact-SQL)**  
  
-   執行 **sp_dropdistpublisher**。 如需詳細資訊，請參閱 [sp_dropdistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [設定 Oracle 發行者](configure-an-oracle-publisher.md)   
 [Oracle 發行概觀](oracle-publishing-overview.md)  
  
  
