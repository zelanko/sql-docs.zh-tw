---
title: 取得並設定備份伺服器-Parallel Data Warehouse |Microsoft Docs
description: 本文說明如何設定非應用裝置的 Windows 系統做為備份伺服器與 Analytics Platform System (APS) 和 Parallel Data Warehouse (PDW) 的備份和還原功能搭配使用。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: cba345eb7a5aec9ef857819a1f0499266649f6e4
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51696947"
---
# <a name="acquire-and-configure-a-backup-server-for-parallel-data-warehouse"></a>取得並設定備份伺服器來進行平行處理資料倉儲
本文說明如何設定非應用裝置的 Windows 系統做為備份伺服器與 Analytics Platform System (APS) 和 Parallel Data Warehouse (PDW) 的備份和還原功能搭配使用。  
  
  
## <a name="Basics"></a>備份伺服器的基本概念  
備份的伺服器：  
  
-   提供及管理由 IT 小組。  
  
-   不需要任何 PDW 專屬的軟體或工具。 PDW 不會安裝到備份伺服器上的任何軟體。  
  
-   位在您自己的非應用裝置機架，且不能置於 AP 設備。  
  
-   可以連接到設備的 InfiniBand 網路。 可以透過 InfiniBand 或乙太網路; 執行備份基於效能考量，建議您使用 InfiniBand。  
  
-   為您自己的客戶網域，不是應用裝置的網域。 您客戶的網域和設備網域之間沒有信任關係。  
  
-   裝載備份的檔案共用，也就是使用伺服器訊息區塊 (SMB) 的應用程式層級的網路通訊協定的 Windows 檔案共用。 備份的檔案共用權限授與 Windows 網域使用者 （通常這是專用的備份使用者） 能夠執行備份和還原共用上的作業。 Windows 網域使用者的使用者名稱和密碼的認證會儲存在 PDW 中，使 PDW 可以執行備份和還原備份的檔案共用上的作業。  
  
## <a name="Step1"></a>步驟 1︰ 決定容量需求  
備份伺服器的系統需求幾乎完全取決於您自己的工作負載。 購買或佈建到備份伺服器之前，您需要找出您的容量需求。 備份伺服器並沒有是專門用來備份，只，只要它會處理您的工作負載的效能和儲存體需求。 您也可以有多個備份的伺服器，才能備份和還原至其中一個多部伺服器的每個資料庫。  
  
使用[備份伺服器容量規劃工作表](backup-capacity-planning-worksheet.md)來協助判斷您的容量需求。  
  
## <a name="Step2"></a>步驟 2： 取得備份的伺服器  
既然您進一步了解您的容量需求，您可以規劃伺服器和您將需要購買或佈建的網路元件。 下列清單中的需求併入您的購買方案，然後購買您的伺服器，或佈建現有的伺服器。  
  
### <a name="software-requirements"></a>軟體需求  
使用 Windows 檔案共用 (SMB) 通訊協定的任何檔案伺服器。  
  
我們建議您 Windows Server 2012 或更多以：  
  
-   取得透過 SMB 的檔案預先配置的效能優勢。  
  
-   您可以使用 立即檔案初始化 (IFI) 來執行備份作業。 您的 IT 團隊管理備份的伺服器上的這項設定。 PDW 組態管理員 (dwconfig.exe) 不會設定或控制 IFI 您備份的伺服器上。 舊版 Windows 沒有 IFI，但仍可用做為備份伺服器。  
  
### <a name="networking-requirements"></a>網路需求  
雖然並非必要，InfiniBand 會是備份伺服器的建議的連線類型。 若要準備將載入伺服器連線到設備 InfiniBand 網路：  
  
1.  打算機架伺服器關閉足以應用裝置，以便您可以將它連接至設備 InfiniBand 切換。 如需 InfiniBand Mellanox 技術的詳細資訊，請參閱白皮書[InfiniBand 簡介](https://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf)。  
  
2.  購買的 Mellanox connectx-3 FDR InfiniBand 單一或雙重連接埠網路介面卡。 建議您在資料傳輸期間購買兩個連接埠的容錯功能的網路介面卡。 高可用性需要兩個連接埠的網路介面卡。  
  
3.  購買的雙連接埠卡片的 2 個 FDR InfiniBand 纜線或單一連接埠卡 1 FDR InfiniBand 纜線。 FDR InfiniBand 纜線會連接到設備的 InfiniBand 網路的載入伺服器。 根據您的環境，載入伺服器與設備 InfiniBand 交換器之間的距離取決纜線長度。  
  
## <a name="Step3"></a>步驟 3： 將伺服器連線到 InfiniBand 網路  
使用下列步驟來載入伺服器連線到 InfiniBand 網路。 如果伺服器不使用 InfiniBand 網路，請略過此步驟。  
  
1.  機架伺服器夠靠近應用裝置，讓您可以將它連接到設備的 InfiniBand 網路。  
  
2.  載入伺服器中安裝 InfiniBand Mellanox connectx-3 FDR InfiniBand 網路介面卡。  
  
3.  使用 FDR 纜線以連接到兩個 InfiniBand 參數的第一個設備的機架中的 InfiniBand 網路介面卡。  
  
4.  安裝並設定適當的 Windows 驅動程式的 InfiniBand 網路介面卡。  
  
    -   Windows 的 InfiniBand 驅動程式開發的 OpenFabrics Alliance InfiniBand 廠商同業協會。  正確的驅動程式可能分散 InfiniBand 網路介面卡。 如果沒有，您可以從 www.openfabrics.org 下載驅動程式。  
  
5.  設定網路介面卡的 InfiniBand 和 DNS 設定。 組態指示，請參閱[設定的 InfiniBand 網路介面卡](configure-infiniband-network-adapters.md)。  
  
## <a name="Step4"></a>步驟 4： 設定備份的檔案共用  
PDW 會透過 UNC 檔案共用來存取備份伺服器。 若要設定檔案共用：  
  
1.  建立資料夾來儲存您的備份在備份伺服器上。  
  
2.  建立檔案共用，稱為備份資料夾的備份共用。  
  
3.  指定或建立您想要用於執行備份及還原的用途在客戶網域中的 Windows 網域帳戶。 基於安全性理由，最好是使用專用的帳戶作為備份的使用者。  
  
4.  新增權限至備份共用，讓只有受信任的帳戶和網域備份的帳戶可以存取，讀取和寫入的共用位置。  
  
5.  將備份的網域帳戶認證新增至 PDW 中。  
  
    例如：  
  
    ```sql  
    EXEC sp_pdw_add_network_credentials '10.192.147.63', 'seattle\david', '********';  
    ```  
  
    如需詳細資訊，請參閱這些預存程序：  
  
    -   [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
    -   [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
## <a name="Step5"></a>步驟 5： 可讓您開始備份您的資料  
您現在已準備好開始備份到備份伺服器的資料。  
  
若要備份的資料，請查詢用戶端用以連線到 SQL Server PDW，然後提交備份或還原資料庫的命令。 使用磁碟 = 子句來指定備份伺服器以及備份位置。  
  
> [!IMPORTANT]  
> 請記得使用備份伺服器的 InfiniBand IP 位址。 否則，資料將會複製透過乙太網路，而不是 InfiniBand。  
  
例如：  
  
```sql  
BACKUP DATABASE Invoices TO DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full';  
  
RESTORE DATABASE Invoices2013Full  
FROM DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full'  
```  
  
如需詳細資訊，請參閱： 
  
-   [備份資料庫](../t-sql/statements/backup-database-parallel-data-warehouse.md)   
  
-   [還原資料庫](../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
## <a name="Security"></a>安全性注意事項  
備份伺服器未加入設備的私人網域。 它是在網路上和您自己的網域和私人的設備網域之間沒有信任關係。  
  
因為 PDW 備份不會儲存在應用裝置上，您的 IT 團隊負責管理備份安全性的所有層面。 比方說，這包括管理備份的資料，用來儲存備份，伺服器的安全性和備份伺服器連線至 AP 設備之網路基礎結構安全性的安全性。  
  
### <a name="manage-network-credentials"></a>管理網路認證  
  
對備份目錄的網路存取權是根據標準 Windows 檔案共用安全性。 之前執行的備份，您必須建立或指定將用於向備份目錄中的 PDW 的 Windows 帳戶。 此 Windows 帳戶必須具備備份目錄之存取、建立及寫入權限。  
  
> [!IMPORTANT]  
> 為了降低您資料的安全性風險，建議您指定一個專門用來執行備份和還原作業的 Windows 帳戶。 請讓此帳戶僅擁有備份位置的權限。  
  
若要將使用者名稱和密碼儲存在 PDW 中，使用[sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)預存程序。 PDW 會使用 Windows 認證管理員，來儲存及加密使用者名稱和密碼，在控制節點上的和計算節點。 備份認證時，不會使用 BACKUP DATABASE 命令來備份。  
  
若要移除 PDW 中的網路認證，請使用[sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)預存程序。  
  
若要列出所有儲存在 SQL Server PDW 中的網路認證，請使用[sys.dm_pdw_network_credentials](../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)動態管理檢視。  
  
### <a name="secure-communications"></a>安全通訊  
  
載入伺服器上的作業可以使用從受信任的內部網路之外的提取資料的 UNC 路徑。 攻擊者在網路上或影響名稱解析的能力可以攔截或修改資料傳送至 PDW。 這代表竄改和資訊洩漏風險。 若要降低竄改的風險：

- 需要登入連線。 
- 在載入伺服器上，設定下列群組原則選項中 Security Settings\Local Policies\Security Options: Microsoft 網路用戶端： 數位簽章通訊 （自動）： 已啟用。  
  
## <a name="see-also"></a>另請參閱  
[備份與還原](backup-and-restore-overview.md)  
  
