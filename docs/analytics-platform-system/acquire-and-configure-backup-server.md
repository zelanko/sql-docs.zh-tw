---
title: 取得 & 設定備份伺服器
description: 本文說明如何將非設備的 Windows 系統設定為備份伺服器，以搭配分析平臺系統（AP）和平行處理資料倉儲（PDW）中的備份和還原功能使用。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: e160c606b19933934ec844b477ffec08475307d8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401488"
---
# <a name="acquire-and-configure-a-backup-server-for-parallel-data-warehouse"></a>取得及設定平行處理資料倉儲的備份伺服器
本文說明如何將非設備的 Windows 系統設定為備份伺服器，以搭配分析平臺系統（AP）和平行處理資料倉儲（PDW）中的備份和還原功能使用。  
  
  
## <a name="backup-server-basics"></a><a name="Basics"></a>備份伺服器基本概念  
備份伺服器：  
  
-   由您自己的 IT 小組提供及管理。  
  
-   不需要任何 PDW 特定軟體或工具。 PDW 不會在備份伺服器上安裝任何軟體。  
  
-   位於您自己的非設備機架中，而且不能放在 AP 設備內。  
  
-   可以連接到設備不會的網路。 備份可以透過未通過或 Ethernet 來執行;基於效能考慮，建議使用「不會」。  
  
-   位於您自己的客戶網域中，而不是設備網域。 您的客戶網域與設備網域之間沒有信任關係。  
  
-   裝載備份檔案共用，這是使用伺服器訊息區（SMB）應用層級網路通訊協定的 Windows 檔案共用。 備份檔案共用許可權會授與 Windows 網域使用者（通常是專用的備份使用者）在共用上執行備份和還原作業的能力。 Windows 網域使用者的「使用者名稱」和「密碼」認證會儲存在 PDW 中，讓 PDW 可以在備份檔案共用上執行備份和還原作業。  
  
## <a name="step-1-determine-capacity-requirements"></a><a name="Step1"></a>步驟1：判斷容量需求  
備份伺服器的系統需求，幾乎完全取決於您自己的工作負載。 在購買或布建備份伺服器之前，您必須先找出您的容量需求。 備份伺服器不需要只專用於備份，只要它會處理工作負載的效能和儲存需求。 您也可以有多部備份伺服器，以便備份和還原每個資料庫到數部伺服器的其中一個。  
  
使用 [[備份伺服器容量規劃] 工作表](backup-capacity-planning-worksheet.md)，以協助判斷您的容量需求。  
  
## <a name="step-2-acquire-the-backup-server"></a><a name="Step2"></a>步驟2：取得備份伺服器  
瞭解您的容量需求之後，您就可以規劃需要購買或布建的伺服器和網路元件。 將下列需求清單併入您的購買方案，然後購買您的伺服器或布建現有的伺服器。  
  
### <a name="software-requirements"></a>軟體需求  
任何使用 Windows 檔案共用（SMB）通訊協定的檔案伺服器。  
  
我們建議 Windows Server 2012 或更高的時間，才能：  
  
-   透過 SMB 取得檔案預先配置的效能優勢。  
  
-   針對備份作業使用立即檔案初始化（IFI）。 您的 IT 小組會在備份伺服器上管理此設定。 PDW Configuration Manager （dwconfig）不會設定或控制備份伺服器上的 IFI。 舊版的 Windows 沒有 IFI，但仍可做為備份伺服器使用。  
  
### <a name="networking-requirements"></a>網路需求  
雖然不是必要的，但對備份伺服器而言，建議的連線類型是 [未使用]。 若要準備將載入伺服器連接到設備不帶的網路：  
  
1.  規劃讓伺服器機架靠近設備，以便您將它連線到設備未充分的交換器。 如需有關有關未受限於之 Mellanox 技術的詳細資訊，請參閱技術白皮書：未通過的[簡介](https://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf)。  
  
2.  購買 Mellanox ConnectX-3 FDR 的單一或雙重埠網路介面卡。 我們建議使用兩個埠來購買網路介面卡，以在資料傳輸期間容錯。 需要兩個埠網路介面卡才能提供高可用性。  
  
3.  購買2個雙埠卡的 FDR 未使用纜線，或單一端口卡的 1 FDR 雙絞線纜線。 FDR 的無法進行的纜線會將載入伺服器連線到設備不會的網路。 根據您的環境，纜線長度取決於載入伺服器和設備未通過交換器之間的距離。  
  
## <a name="step-3-connect-the-server-to-the-infiniband-networks"></a><a name="Step3"></a>步驟3：將伺服器連接到不會的網路  
使用下列步驟，將載入伺服器連線到不會的網路。 如果伺服器不是使用不會的網路，請略過此步驟。  
  
1.  讓伺服器靠近設備，以便您可以將它連接到設備不會的網路。  
  
2.  將無法執行的 Mellanox ConnectX-3 FDR 的網路介面卡安裝到載入伺服器。  
  
3.  使用 FDR 纜線將未使用的網路介面卡連接到第一個設備機架中的兩個未使用的交換器之一。  
  
4.  為「未設定的網路介面卡」安裝並設定適當的 Windows 驅動程式。  
  
    -   適用于 Windows 的不駕駛驅動程式是由 OpenFabrics 聯盟所開發，這是一家不受駕駛廠商的產業聯盟。  正確的驅動程式可能已與您的未使用網路介面卡一起散發。 如果不是，可以從 www.openfabrics.org 下載驅動程式。  
  
5.  設定網路介面卡的「未通過」和「DNS」設定。 如需設定指示，請參閱設定不確定的[網路介面卡](configure-infiniband-network-adapters.md)。  
  
## <a name="step-4-configure-the-backup-file-share"></a><a name="Step4"></a>步驟4：設定備份檔案共用  
PDW 會透過 UNC 檔案共用存取備份伺服器。 若要設定檔案共用：  
  
1.  在備份伺服器上建立用來儲存備份的資料夾。  
  
2.  為 [備份] 資料夾建立檔案共用（稱為「備份共用」）。  
  
3.  在您的客戶網域中指定或建立要用於執行備份和還原的 Windows 網域帳戶。 基於安全性理由，最好使用專用帳戶做為備份使用者。  
  
4.  將許可權新增至備份共用，讓只有信任的帳戶和網域備份帳戶可以存取、讀取及寫入共用位置。  
  
5.  將備份網域帳號憑證新增至 PDW。  
  
    例如：  
  
    ```sql  
    EXEC sp_pdw_add_network_credentials '10.192.147.63', 'seattle\david', '********';  
    ```  
  
    如需詳細資訊，請參閱下列預存程式：  
  
    -   [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
    -   [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
## <a name="step-5-start-backing-up-your-data"></a><a name="Step5"></a>步驟5：開始備份您的資料  
您現在已準備好開始將資料備份到備份伺服器。  
  
若要備份資料，請使用查詢用戶端連接到 SQL Server PDW，然後提交備份資料庫或還原資料庫命令。 使用 DISK = 子句來指定備份伺服器和備份位置。  
  
> [!IMPORTANT]  
> 請記得使用備份伺服器的不會的 IP 位址。 否則，資料將會透過乙太網路複製，而不是自動處理。  
  
例如：  
  
```sql  
BACKUP DATABASE Invoices TO DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full';  
  
RESTORE DATABASE Invoices2013Full  
FROM DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full'  
```  
  
如需詳細資訊，請參閱： 
  
-   [BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)   
  
-   [RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
## <a name="security-notices"></a><a name="Security"></a>安全性注意事項  
備份伺服器未加入設備的私人網域。 它位於您自己的網路中，而且您自己的網域和私人設備網域之間沒有信任關係。  
  
由於 PDW 備份不會儲存在應用裝置上，因此您的 IT 小組會負責管理備份安全性的所有層面。 例如，這包括管理備份資料的安全性、用來儲存備份之伺服器的安全性，以及將備份伺服器連接到 AP 設備的網路基礎結構安全性。  
  
### <a name="manage-network-credentials"></a>管理網路認證  
  
對備份目錄的網路存取權是根據標準 Windows 檔案共用安全性。 在執行備份之前，您必須先建立或指定 Windows 帳戶，以用來向備份目錄驗證 PDW。 此 Windows 帳戶必須具備備份目錄之存取、建立及寫入權限。  
  
> [!IMPORTANT]  
> 為了降低您資料的安全性風險，建議您指定一個專門用來執行備份和還原作業的 Windows 帳戶。 請讓此帳戶僅擁有備份位置的權限。  
  
若要在 PDW 中儲存使用者名稱和密碼，請使用[sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)預存程式。 PDW 會使用 Windows 認證管理員來儲存及加密控制節點和計算節點上的使用者名稱和密碼。 備份認證時，不會使用 BACKUP DATABASE 命令來備份。  
  
若要從 PDW 移除網路認證，請使用[sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)預存程式。  
  
若要列出 SQL Server PDW 中儲存的所有網路認證，請使用[dm_pdw_network_credentials](../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)動態管理檢視。  
  
### <a name="secure-communications"></a>安全通訊  
  
載入伺服器上的作業可以使用 UNC 路徑，從受信任的內部網路外部提取資料。 網路上的攻擊者或具有影響名稱解析的能力，可以攔截或修改傳送至 PDW 的資料。 這會帶來一種篡改和資訊洩漏風險。 若要協助降低篡改的風險：

- 需要登入連接。 
- 在載入伺服器上，于 [安全性] [本機] [保護選項： Microsoft 網路用戶端：數位簽署通訊（一律）：啟用] 中設定下列群組原則選項。  
  
## <a name="see-also"></a>另請參閱  
[備份與還原](backup-and-restore-overview.md)  
  
