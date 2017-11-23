---
title: "取得和設定來載入伺服器 (SQL Server PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "取得和設定來載入伺服器送出到 SQL Server Parallel Data Warehouse 的資料載入非應用裝置 Windows 系統。"
ms.date: 10/20/2016
ms.topic: article
ms.assetid: a434b174-a818-4f73-b218-264619bab664
caps.latest.revision: "19"
ms.openlocfilehash: 05747889f905e1f827a87cc0ad53ace62a911922
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="acquire-and-configure-a-loading-server"></a>取得和設定來載入伺服器
本主題描述如何取得及載入伺服器設定為在非應用裝置的 Windows 系統提交資料載入到 SQL Server Parallel Data Warehouse (PDW)。  
  
## <a name="Basics"></a>基本概念  
載入伺服器：  
  
-   沒有為單一伺服器。 您可以與多個載入伺服器同時載入。  
  
-   會提供和管理您自己的 IT 團隊。 您可能已經有可用於將資料載入 PDW 的伺服器。  
  
-   位於您自己的非應用裝置機架，並不能放 Analytics Platform System 應用裝置內。  
  
-   連線到透過設備 InfiniBand 網路中，或透過乙太網路應用裝置。 效能，我們建議使用 InfiniBand。  
  
-   是在您自己客戶網域中，不是應用裝置的網域。 客戶網域和應用裝置網域之間沒有信任關係。  
  
## <a name="Step1"></a>步驟 1： 決定的容量需求  
載入系統都可以設計成做為一或多個執行並行載入，載入伺服器。 每個載入伺服器沒有專門只載入時，只要它會處理您的工作負載的效能和儲存需求。  
  
載入伺服器的系統需求幾乎完全取決於您自己的工作負載。 使用[載入伺服器容量規劃工作表](loading-server-capacity-planning-worksheet.md)以協助判斷您的容量需求。  
  
## <a name="Step2"></a>步驟 2： 取得 sServer  
既然您進一步了解您的容量需求，您可以規劃伺服器和網路元件，您將需要購買或佈建。 以下清單中的需求併入您購買的計劃，然後購買您的伺服器，或提供現有的伺服器。  
  
### <a name="R"></a>軟體需求  
支援的作業系統：  
  
-   Windows Server 2012 或 Windows Server 2012 R2。 這些作業系統需要 FDR 網路介面卡。  
  
-   Windows Server 2008 R2。 這個作業系統需要 DDR 網路介面卡。  
  
伺服器必須使用 EN-US 地區設定，才能使用 dwloader 載入命令列工具。 dwloader 不支援其他地區設定。  
  
### <a name="networking-requirements-for-windows-server-2012-and-windows-server-2012-r2"></a>Windows Server 2012 和 Windows Server 2012 R2 的網路需求  
雖然不需要載入，但是 InfiniBand 是建議的連線類型來載入伺服器。 為了達到最佳效能，使用 Windows Server 2012 或 Windows Server 2012 R2 和 FDR InfiniBand 網路介面卡來載入伺服器連線至應用裝置 InfiniBand 網路。  
  
若要準備的 Windows Server 2012 或 Windows Server 2012 R2 InfiniBand 連接：  
  
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
  
## <a name="Step4"></a>步驟 4： 安裝載入工具  
用戶端工具是可從 Microsoft 下載中心下載。 

若要安裝 dwloader，執行 dwloader 安裝用戶端工具中。
  
如果您打算使用載入的 Integration Services，您必須安裝 Integration Services 和 Integration Services 目的地配接器。 用戶端工具中使用配接器。

<!-- To install the des[Install Integration Services Destination Adapters](install-integration-services-destination-adapters.md). 
--> 
  
## <a name="Step5"></a>步驟 5： 開始載入  
現在您已經準備好開始載入資料。 如需詳細資訊，請參閱：  
  
1.  [dwloader 命令列載入工具](dwloader.md)  
  
2.  [負載概觀](load-overview.md)  
  
## <a name="performance"></a>效能  
載入 Windows Server 2012 和更新版本的效能最佳，開啟立即檔案初始化，因此資料會覆寫時，系統不會覆寫現有的資料加上零。 如果這是安全性風險，因為之前的資料仍存在於磁碟上，請務必關閉立即檔案初始化。  
  
## <a name="Security"></a>安全性注意事項  
因為要載入的資料不會儲存在應用裝置中，您的 IT 團隊負責管理您載入資料的安全性的所有層面。 比方說，這包括管理要載入之資料的安全性、 用來儲存負載、 伺服器的安全性和載入伺服器連線到 SQL Server PDW 應用裝置的網路基礎結構的安全性。  
  
> [!IMPORTANT]  
> 它是特別重要，保護將會使用 dwloader 載入命令列工具每個載入伺服器。 當 dwloader 載入資料時，第一次驗證使用的控制節點，然後在成功驗證之後它移動資料載入伺服器從直接用於運算節點資料通道上。 在每個載入伺服器和每個計算節點之間手動搖晃期間不會發生憑證驗證。 這會保留運算節點公開給每個資料通道，在載入時攔截的攻擊。 這些攻擊可能會遭竄改的資料和/或資訊洩漏。  
  
若要減少資料的安全性風險，我們建議下列各項︰  
  
-   指定僅用於將資料載入 PDW 的同一個 Windows 帳戶。 允許此帳戶有權載入位置與其他無處可去。  
  
-   指定一個 PDW 使用者具有權限來載入資料。 根據您的安全性需求，您可能會有一個指定的使用者，每個資料庫。  
  
-   載入伺服器上的作業可以接受從中提取資料從受信任內部網路之外的 UNC 路徑。 與網路上或能力影響名稱解析攻擊者可以攔截或修改傳送至 SQL Server PDW 資料。 這會遭到竄改及資訊外洩風險。 應該降低遭到竄改，要求登入連接。 若要降低此風險，設定下列群組原則選項**安全性 \ 原則 \ 安全性選項**載入伺服器上： **Microsoft 網路用戶端： 數位簽章通訊 （自動）：已啟用**  
  
-   關閉 Windows Server 2012 和更新版本的立即檔案初始化。 這是權衡考量效能和安全性，如 「 效能 」 區段中所述。 您需要決定哪一種最佳根據您的安全性需求。  
  
## <a name="see-also"></a>請參閱＜  
[備份和還原的概觀](backup-and-restore-overview.md)  
  
