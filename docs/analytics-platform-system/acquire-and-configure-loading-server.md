---
title: 取得 & 設定載入伺服器
description: 本文說明如何取得並設定載入伺服器做為非設備的 Windows 系統，以將資料載入提交至平行處理資料倉儲（PDW）。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ef49bb86c8e16600f2ff1bf2d1c7a92ecc5af964
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401480"
---
# <a name="acquire-and-configure-a-loading-server-for-parallel-data-warehouse"></a>取得及設定平行處理資料倉儲的載入伺服器
本文說明如何取得並設定載入伺服器做為非設備的 Windows 系統，以將資料載入提交至平行處理資料倉儲（PDW）。  
  
## <a name="basics"></a><a name="Basics"></a>基本概念  
載入伺服器：  
  
-   不一定要是單一伺服器。 您可以同時載入多個載入伺服器。  
  
-   由您自己的 IT 小組提供及管理。 您可能已經有一部伺服器，可以用來將資料載入 PDW。  
  
-   位於您自己的非設備機架中，不能放在分析平臺系統裝置內。  
  
-   會透過設備不會的網路或經由 Ethernet 連接到設備。 基於效能，我們建議使用 [未通過]。  
  
-   位於您自己的客戶網域中，而不是設備網域。 您的客戶網域與設備網域之間沒有信任關係。  
  
## <a name="step-1-determine-capacity-requirements"></a><a name="Step1"></a>步驟1：判斷容量需求  
載入系統可以設計為一或多個執行並行載入的載入伺服器。 每個載入伺服器都不需要專用於載入，只要它會處理工作負載的效能和儲存需求。  
  
載入伺服器的系統需求，幾乎完全取決於您自己的工作負載。 使用 [[載入伺服器容量規劃] 工作表](loading-server-capacity-planning-worksheet.md)，以協助判斷您的容量需求。  
  
## <a name="step-2-acquire-the-sserver"></a><a name="Step2"></a>步驟2：取得 Server  
瞭解您的容量需求之後，您就可以規劃需要購買或布建的伺服器和網路元件。 將下列需求清單併入您的購買方案，然後購買您的伺服器或布建現有的伺服器。  
  
### <a name="software-requirements"></a><a name="R"></a>軟體需求  
支援的作業系統：  
  
-   Windows Server 2012 或 Windows Server 2012 R2。 這些作業系統需要 FDR 網路介面卡。  
  
-   Windows Server 2008 R2。 此 OS 需要 DDR 網路介面卡。  
  
伺服器必須使用 EN-US 地區設定，才能使用 dwloader 命令列載入工具。 dwloader 不支援其他地區設定。  
  
### <a name="networking-requirements-for-windows-server-2012-and-windows-server-2012-r2"></a>Windows Server 2012 和 Windows Server 2012 R2 的網路需求  
雖然不需要進行載入，但在載入伺服器時，建議的連線類型是「不適用」。 為了達到最佳效能，請使用 Windows Server 2012 或 Windows Server 2012 R2，以及 FDR 的網路介面卡，將載入伺服器連線到設備不會的網路。  
  
若要準備 Windows Server 2012 或 Windows Server 2012 R2 不會連線的連線：  
  
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
  
## <a name="step-4-install-the-loading-tools"></a><a name="Step4"></a>步驟4：安裝載入工具  
用戶端工具可從 Microsoft 下載中心下載。 

若要安裝 dwloader，請從用戶端工具執行 dwloader 安裝。
  
如果您打算使用 Integration Services 進行載入，就必須安裝 Integration Services 和 Integration Services 目的地介面卡。 這些介面卡可在用戶端工具中取得。

<!-- To install the des[Install Integration Services Destination Adapters](install-integration-services-destination-adapters.md). 
--> 
  
## <a name="step-5-start-loading"></a><a name="Step5"></a>步驟5：開始載入  
您現在已準備好開始載入資料。 如需詳細資訊，請參閱：  
  
1.  [dwloader 命令列載入工具](dwloader.md)  
  
2.  [負載總覽](load-overview.md)  
  
## <a name="performance"></a>效能  
如需 Windows Server 2012 和更高的效能，請開啟立即檔案初始化，以便在覆寫資料時，作業系統不會以零覆寫現有資料。 如果這是安全性風險，因為先前的資料仍然存在於磁片上，請務必關閉立即檔案初始化。  
  
## <a name="security-notices"></a><a name="Security"></a>安全性注意事項  
由於要載入的資料不會儲存在應用裝置上，因此您的 IT 小組會負責管理安全性的所有層面，以便載入您的資料。 例如，這包括管理要載入的資料安全性、用來儲存負載的伺服器安全性，以及將載入伺服器連線到 SQL Server PDW 設備的網路基礎結構安全性。  
  
> [!IMPORTANT]  
> 特別重要的是保護將使用 dwloader 命令列載入工具的每一部載入伺服器。 當 dwloader 載入資料時，它會先向控制節點進行驗證，然後在驗證成功之後，將資料從載入伺服器直接移到計算節點上的資料通道。 在每個載入伺服器與每個計算節點之間的右手搖動期間，不會發生憑證驗證。 這會讓計算節點在載入時，針對每個資料通道的潛在攔截式攻擊而公開。 這些攻擊可能會導致資料洩露和/或資訊洩漏。  
  
為了降低資料的安全性風險，我們建議下列事項：  
  
-   指定一個 Windows 帳戶，僅用於將資料載入 PDW 的目的。 允許此帳戶具有載入位置的許可權，以及其他地方。  
  
-   指定具有載入資料許可權的一個 PDW 使用者。 根據您的安全性需求，每個資料庫可以有一個特定的使用者。  
  
-   載入伺服器上的作業可以接受 UNC 路徑，從受信任的內部網路外部提取資料。 而網路上的攻擊者，或能夠影響名稱解析的能力，可以攔截或修改傳送至 SQL Server PDW 的資料。 這會帶來一種篡改和資訊洩漏風險。 您應該透過要求登入連接來減輕篡改。 若要協助降低此風險，請在載入伺服器上的 [安全性] [本機**保護] 選項**中，設定下列群組原則選項： [ **Microsoft 網路用戶端：數位簽章通訊（一律）]： [已啟用**]  
  
-   關閉 Windows Server 2012 和更高的檔案立即初始化。 這是效能與安全性之間的取捨，如效能一節中所述。 您必須根據您的安全性需求來決定最佳程度。  
  
## <a name="see-also"></a>另請參閱  
[備份與還原總覽](backup-and-restore-overview.md)  
  
