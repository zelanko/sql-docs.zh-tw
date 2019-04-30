---
title: 取得並設定載入伺服器-Parallel Data Warehouse |Microsoft Docs
description: 本文說明如何取得和設定載入伺服器做為非應用裝置 Windows 系統，來提交資料載入至 Parallel Data Warehouse (PDW)。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: da404aa881f3ff7af26a681751aae12a45f2628f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63231100"
---
# <a name="acquire-and-configure-a-loading-server-for-parallel-data-warehouse"></a>取得並設定載入伺服器來進行平行處理資料倉儲
本文說明如何取得和設定載入伺服器做為非應用裝置 Windows 系統，來提交資料載入至 Parallel Data Warehouse (PDW)。  
  
## <a name="Basics"></a>基本概念  
載入伺服器中：  
  
-   沒有要在單一伺服器。 您可以與多個載入伺服器同時載入。  
  
-   提供及管理由 IT 小組。 您可能已經有可用於將資料載入 PDW 的伺服器。  
  
-   位在您自己的非應用裝置機架，且不能放在 Analytics Platform System appliance。  
  
-   連線到透過設備 InfiniBand 網路，或透過乙太網路應用裝置。 如需效能，我們建議使用 InfiniBand。  
  
-   為您自己的客戶網域，不是應用裝置的網域。 您客戶的網域和設備網域之間沒有信任關係。  
  
## <a name="Step1"></a>步驟 1:決定容量需求  
正在載入系統可以設計成一或多個執行並行載入，載入伺服器。 每個載入伺服器沒有專用只載入時，只要它會處理您的工作負載的效能和儲存體需求。  
  
載入伺服器的系統需求幾乎完全取決於您自己的工作負載。 使用[載入伺服器容量規劃工作表](loading-server-capacity-planning-worksheet.md)來協助判斷您的容量需求。  
  
## <a name="Step2"></a>步驟 2:取得 Server  
既然您進一步了解您的容量需求，您可以規劃伺服器和您將需要購買或佈建的網路元件。 下列清單中的需求併入您的購買方案，然後購買您的伺服器，或佈建現有的伺服器。  
  
### <a name="R"></a>軟體需求  
支援的作業系統：  
  
-   Windows Server 2012 或 Windows Server 2012 R2。 這些作業系統需要 FDR 網路介面卡。  
  
-   Windows Server 2008 R2. 這個作業系統需要 DDR 網路介面卡。  
  
伺服器必須使用 EN-US 地區設定，才能使用 dwloader 命令列載入工具。 dwloader 不支援其他地區設定。  
  
### <a name="networking-requirements-for-windows-server-2012-and-windows-server-2012-r2"></a>Windows Server 2012 和 Windows Server 2012 R2 的網路需求  
雖然不需要載入，InfiniBand 是建議的連線類型來載入伺服器。 為了達到最佳效能，使用 Windows Server 2012 或 Windows Server 2012 R2 和 FDR InfiniBand 網路介面卡來載入伺服器與設備的 InfiniBand 網路。  
  
若要準備 Windows Server 2012 或 Windows Server 2012 R2 InfiniBand 連線：  
  
1.  打算機架伺服器關閉足以應用裝置，以便您可以將它連接至設備 InfiniBand 切換。 如需 InfiniBand Mellanox 技術的詳細資訊，請參閱白皮書[InfiniBand 簡介](https://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf)。  
  
2.  購買的 Mellanox connectx-3 FDR InfiniBand 單一或雙重連接埠網路介面卡。 建議您在資料傳輸期間購買兩個連接埠的容錯功能的網路介面卡。 高可用性需要兩個連接埠的網路介面卡。  
  
3.  購買的雙連接埠卡片的 2 個 FDR InfiniBand 纜線或單一連接埠卡 1 FDR InfiniBand 纜線。 FDR InfiniBand 纜線會連接到設備的 InfiniBand 網路的載入伺服器。 根據您的環境，載入伺服器與設備 InfiniBand 交換器之間的距離取決纜線長度。  
  
## <a name="Step3"></a>步驟 3:將伺服器連線到 InfiniBand 網路  
使用下列步驟來載入伺服器連線到 InfiniBand 網路。 如果伺服器不使用 InfiniBand 網路，請略過此步驟。  
  
1.  機架伺服器夠靠近應用裝置，讓您可以將它連接到設備的 InfiniBand 網路。  
  
2.  載入伺服器中安裝 InfiniBand Mellanox connectx-3 FDR InfiniBand 網路介面卡。  
  
3.  使用 FDR 纜線以連接到兩個 InfiniBand 參數的第一個設備的機架中的 InfiniBand 網路介面卡。  
  
4.  安裝並設定適當的 Windows 驅動程式的 InfiniBand 網路介面卡。  
  
    -   Windows 的 InfiniBand 驅動程式開發的 OpenFabrics Alliance InfiniBand 廠商同業協會。  正確的驅動程式可能分散 InfiniBand 網路介面卡。 如果沒有，您可以從 www.openfabrics.org 下載驅動程式。  
  
5.  設定網路介面卡的 InfiniBand 和 DNS 設定。 組態指示，請參閱[設定的 InfiniBand 網路介面卡](configure-infiniband-network-adapters.md)。  
  
## <a name="Step4"></a>步驟 4:安裝載入工具  
用戶端工具則可從 Microsoft 下載中心下載。 

若要安裝 dwloader，執行 dwloader 安裝用戶端工具中。
  
如果您打算使用載入的 Integration Services，您必須安裝 Integration Services 和 Integration Services 目的地配接器。 配接器是用戶端工具中可用的。

<!-- To install the des[Install Integration Services Destination Adapters](install-integration-services-destination-adapters.md). 
--> 
  
## <a name="Step5"></a>步驟 5:啟動載入  
您現在已準備好開始載入資料。 如需詳細資訊，請參閱：  
  
1.  [dwloader 命令列載入工具](dwloader.md)  
  
2.  [載入概觀](load-overview.md)  
  
## <a name="performance"></a>效能  
最佳載入效能及更新版本 Windows Server 2012 上，開啟立即檔案初始化，因此資料會覆寫時，作業系統不會覆寫現有的資料以零。 如果這是有安全性風險，因為先前的資料仍存在於磁碟上，請務必關閉檔案立即初始化。  
  
## <a name="Security"></a>安全性注意事項  
因為要載入的資料不會儲存在應用裝置上，您的 IT 團隊負責管理您的資料載入的安全性的所有層面。 比方說，這包括管理要載入之資料的安全性、 用來儲存載入伺服器的安全性和載入伺服器連線到 SQL Server PDW 應用裝置的網路基礎結構的安全性。  
  
> [!IMPORTANT]  
> 它是特別重要，保護將使用 dwloader 命令列載入工具每個載入伺服器。 當 dwloader 載入資料時，它首先會驗證與控制 節點中，之後，再在成功驗證之後移資料載入伺服器從直接至計算節點資料通道上。 憑證驗證就不會在每個載入伺服器和每個計算節點之間手動搖晃。 這可讓計算節點可能的攔截層攻擊，在載入每個資料通道上公開。 這些攻擊可能會導致遭竄改的資料和/或導致資訊洩漏。  
  
若要降低安全性風險，您的資料，我們建議下列各項：  
  
-   指定一個專門用來將資料載入 PDW 用的 Windows 帳戶。 允許此帳戶有權限才能載入位置和地方。  
  
-   指定一個 PDW 使用者具有將資料的權限。 根據您的安全性需求，您可以有一個特定的使用者，每個資料庫。  
  
-   載入伺服器上的作業可以接受從中提取資料從受信任的內部網路之外的 UNC 路徑。 和攻擊者在網路上或影響名稱解析的能力可以攔截或修改資料傳送至 SQL Server PDW。 這代表竄改和資訊洩漏風險。 應該需要登入連接降低遭到竄改。 若要降低此風險，請在中設定下列群組原則選項**Security Settings\Local Policies\Security Options**載入伺服器上：**Microsoft 網路用戶端：數位簽署通訊 （自動）：已啟用**  
  
-   關閉 Windows Server 2012 和更新版本的立即檔案初始化。 在 [效能] 區段中所述，這會是效能與安全性之間有所取捨。 您需要決定哪一種最佳根據您的安全性需求。  
  
## <a name="see-also"></a>另請參閱  
[備份與還原概觀](backup-and-restore-overview.md)  
  
