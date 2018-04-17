---
title: 取得和設定的 APS PDW 備份伺服器
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: 設定非應用裝置的 Windows 系統做為備份的伺服器，用於備份和還原功能 Analytics Platform System (APS) 和 SQL Server Parallel Data Warehouse (PDW)。
ms.date: 10/20/2016
ms.topic: article
caps.latest.revision: 20
ms.assetid: f8b769fe-c864-4d65-abcb-a9a287061702
ms.openlocfilehash: 564a70d5fa483f2c34ef2598213a2c22074daf80
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="acquire-and-configure-a-backup-server"></a>取得和設定備份伺服器
本主題描述如何將非應用裝置的 Windows 系統設定為與 Analytics Platform System (AP) 的備份和還原功能搭配使用的備份伺服器和 SQL Server Parallel Data Warehouse (PDW)。  
  
  
## <a name="Basics"></a>備份伺服器的基本概念  
備份的伺服器：  
  
-   會提供和管理您自己的 IT 團隊。  
  
-   不需要任何 PDW 專屬的軟體或工具。 PDW 不會安裝到備份伺服器上的任何軟體。  
  
-   位於您自己的非應用裝置機架，並不能放 AP 應用裝置內。  
  
-   可以連接至應用裝置 InfiniBand 網路。 可以透過 InfiniBand 或乙太網路; 執行備份基於效能考量，建議您使用 InfiniBand。  
  
-   是在您自己客戶網域中，不是應用裝置的網域。 客戶網域和應用裝置網域之間沒有信任關係。  
  
-   裝載備份的檔案共用，也就是使用伺服器訊息區塊 (SMB) 應用程式層級的網路通訊協定的 Windows 檔案共用。 備份檔案共用權限授與 Windows 網域使用者 （通常這是固定的備份使用者） 執行備份和還原作業的共用上的能力。 Windows 網域使用者的使用者名稱和密碼認證會儲存在 PDW 中，使 PDW 可以執行備份和還原備份的檔案共用上的作業。  
  
## <a name="Step1"></a>步驟 1： 決定容量需求  
備份伺服器的系統需求幾乎完全取決於您自己的工作負載。 購買或佈建到備份伺服器之前，您需要找出您的容量需求。 備份伺服器不必是專門用來備份，只，只要它會處理您的工作負載的效能和儲存體需求。 您也可以讓多個備份的伺服器，才能備份和還原至其中一個多部伺服器的每個資料庫。  
  
使用[備份伺服器容量規劃工作表](backup-capacity-planning-worksheet.md)以協助判斷您的容量需求。  
  
## <a name="Step2"></a>步驟 2： 取得備份的伺服器  
既然您進一步了解您的容量需求，您可以規劃伺服器和網路元件，您將需要購買或佈建。 以下清單中的需求併入您購買的計劃，然後購買您的伺服器，或提供現有的伺服器。  
  
### <a name="software-requirements"></a>軟體需求  
使用 Windows 檔案共用 (SMB) 通訊協定的任何檔案伺服器。  
  
我們建議您 Windows Server 2012 或以超出：  
  
-   取得透過 SMB 的檔案預先配置的效能優勢。  
  
-   使用立即檔案初始化 (IFI) 來執行備份作業。 您的 IT 團隊會管理此備份伺服器上的設定。 PDW 組態管理員 (dwconfig.exe) 不會設定，或控制 IFI 您備份的伺服器上。 舊版 Windows 沒有 IFI，，但仍然可以做為備份的伺服器使用。  
  
### <a name="networking-requirements"></a>網路需求  
雖然並非必要，InfiniBand 是備份伺服器的建議的連線類型。 若要準備將載入伺服器連線至應用裝置 InfiniBand 網路：  
  
1.  機架的伺服器計劃接近應用裝置，讓您可以將它連接到切換 InfiniBand 應用裝置。 如需 InfiniBand Mellanox 技術的詳細資訊，請參閱白皮書，[簡介 InfiniBand](http://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf)。  
  
2.  購買 Mellanox connectx-3 FDR InfiniBand 單一或雙連接埠的網路介面卡。 我們建議您在資料傳輸期間購買的容錯功能的兩個連接埠的網路介面卡。 高可用性需要兩個連接埠的網路介面卡。  
  
3.  購買的雙連接埠卡 2 FDR InfiniBand 纜線或單一連接埠卡 1 FDR InfiniBand 纜線。 FDR InfiniBand 纜線將設備 InfiniBand 網路連接來載入伺服器。 纜線長度會根據您的環境定來載入伺服器和應用裝置 InfiniBand 交換器之間的距離。  
  
## <a name="Step3"></a>步驟 3： 將伺服器連線到 InfiniBand 網路  
使用下列步驟來連接至的 InfiniBand 網路載入伺服器。 如果伺服器未使用的 InfiniBand 網路，請略過此步驟。  
  
1.  機架伺服器關閉足以應用裝置，您可以將它連接至應用裝置 InfiniBand 網路。  
  
2.  載入伺服器中安裝 InfiniBand Mellanox connectx-3 FDR InfiniBand 網路介面卡。  
  
3.  使用 FDR 纜線連接到其中的第一個設備的機架中的兩個 InfiniBand 參數的 InfiniBand 網路介面卡。  
  
4.  安裝和設定適當的 InfiniBand 網路介面卡的 Windows 驅動程式。  
  
    -   InfiniBand 適用於 Windows 的驅動程式會由 OpenFabrics 聯盟，InfiniBand 供應商的產業協會開發。  正確的驅動程式可能已發佈 InfiniBand 網路介面卡。 如果沒有，您可以從 www.openfabrics.org 下載驅動程式。  
  
5.  設定網路介面卡的 InfiniBand 和 DNS 設定。 組態指示，請參閱[設定 InfiniBand 網路介面卡](configure-infiniband-network-adapters.md)。  
  
## <a name="Step4"></a>步驟 4： 設定備份的檔案共用  
PDW 會透過 UNC 檔案共用存取備份伺服器。 若要設定檔案共用：  
  
1.  儲存備份的備份伺服器上建立資料夾。  
  
2.  建立檔案共用，稱為備份共用，備份的資料夾。  
  
3.  指定或您想要執行的備份和還原的用途的客戶網域中建立的 Windows 網域帳戶。 基於安全性理由，所以最好先備份使用者身分使用的專用的帳戶。  
  
4.  加入備份的權限共用，讓只有受信任的帳戶和網域的備份帳戶可以存取，讀取和寫入的共用位置。  
  
5.  加入 PDW 備份網域帳戶認證。  
  
    例如：  
  
    ```sql  
    EXEC sp_pdw_add_network_credentials '10.192.147.63', 'seattle\david', '********';  
    ```  
  
    如需詳細資訊，請參閱這些預存程序：  
  
    -   [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
    -   [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
## <a name="Step5"></a>步驟 5： 開始備份您的資料  
您可立即開始備份到備份伺服器資料。  
  
若要備份資料，請使用查詢用戶端連接到 SQL Server PDW，然後提交 備份或還原資料庫命令。 使用磁碟 = 子句來指定備份伺服器和備份位置。  
  
> [!IMPORTANT]  
> 請記得使用備份伺服器的 InfiniBand IP 位址。 否則，會透過乙太網路，而不是 InfiniBand 複製資料。  
  
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
備份伺服器未加入專用網域，該裝置。 它在網路上也有自己的網域和私人應用裝置的網域之間沒有信任關係。  
  
因為 PDW 備份不會儲存在應用裝置，您的 IT 團隊負責管理備份安全性的各個層面。 比方說，這包括管理備份的資料，用來儲存備份，伺服器的安全性和備份的伺服器連線到 AP 應用裝置的網路基礎結構安全性的安全性。  
  
### <a name="manage-network-credentials"></a>管理網路認證  
  
對備份目錄的網路存取權是根據標準 Windows 檔案共用安全性。 之前執行的備份，您必須建立或指定要用於驗證 PDW 備份目錄的 Windows 帳戶。 此 Windows 帳戶必須具備備份目錄之存取、建立及寫入權限。  
  
> [!IMPORTANT]  
> 為了降低您資料的安全性風險，建議您指定一個專門用來執行備份和還原作業的 Windows 帳戶。 請讓此帳戶僅擁有備份位置的權限。  
  
若要將使用者名稱和密碼儲存在 PDW 中，使用[sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)預存程序。 PDW 使用 Windows 認證管理員來儲存和加密使用者名稱和密碼的控制節點及計算節點。 備份認證時，不會使用 BACKUP DATABASE 命令來備份。  
  
若要移除 PDW 網路認證，請使用[sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)預存程序。  
  
若要列出所有儲存在 SQL Server PDW 的網路認證，請使用[sys.dm_pdw_network_credentials](../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)動態管理檢視。  
  
### <a name="secure-communications"></a>安全通訊  
  
載入伺服器上的作業可以使用受信任內部網路之外的提取資料的 UNC 路徑。 攻擊者在網路上或影響名稱解析的能力可以攔截或修改資料傳送至 PDW。 這會遭到竄改及資訊外洩風險。 若要降低竄改的風險：

- 需要登入連接。 
- 在載入伺服器上，設定下列群組原則選項中安全性 \ 原則 \ 安全性選項： Microsoft 網路用戶端： 數位簽章通訊 （自動）： 已啟用。  
  
## <a name="see-also"></a>另請參閱  
[備份與還原](backup-and-restore-overview.md)  
  
