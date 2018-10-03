---
title: 使用 VPN 透過網際網路發行資料 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- VPNs [SQL Server replication]
- Web publishing [SQL Server replication], VPNs
- Internet [SQL Server replication], VPNs
ms.assetid: 9ffb6546-9973-4574-aaa0-8fe0017e3601
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ae02e735defc099c0074c17a97e103d3ea938670
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218469"
---
# <a name="publish-data-over-the-internet-using-vpn"></a>使用 VPN 透過網際網路發行資料
  虛擬私人網路 (Virtual Private Networking，VPN) 技術可以讓使用者在家裏、分公司辦公室、遠端用戶端以及其他公司透過網際網路連接到公司網路進行工作，同時保有安全的通訊。 使用者可以使用「Windows 驗證」(Windows Authentication)，就好像他們是在區域網路 (Area Network，LAN) 一樣。 所有類型的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫都可以透過 VPN 複寫資料，但如果您使用合併式複寫，請考慮使用 Web 同步處理，因為 Web 同步處理會省去使用 VPN 的需求。 如需詳細資訊，請參閱 [Web Synchronization for Merge Replication](web-synchronization-for-merge-replication.md)。  
  
 VPN 包含用戶端軟體，因此電腦可以透過網際網路 (在某些特殊情況下，甚至是內部網路) 連接到專用電腦或伺服器中的軟體。 也可以選擇對連線兩端加密及使用者驗證方法。 透過網際網路的 VPN 連接在邏輯上的操作類似站台之間的「廣域網路」(WAN) 連結。  
  
 VPN 透過另一個網路來連接其網路元件。 若要進行連接，使用者可使用如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Point-to-Point Tunneling Protocol (PPTP) 或 Layer Two Tunneling Protocol (L2TP) 之類的通訊協定穿過網際網路或其他共用網路。 這一程序提供的安全性和功能，與先前只能在私人網路使用的安全性和功能相同。 PPTP 在 Microsoft Windows NT 4.0 版和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 2000 (及更新版本) 作業系統中有提供；L2TP 在 Windows 2000 及更新版本中有提供。  
  
 使用者看不到網際網路的中間路由基礎結構，資料像是透過專用私人連結來傳送一樣。 就使用者而言，VPN 是使用者電腦和公司伺服器之間的點對點連線。  
  
 當您將遠端用戶端設定成使用 VPN 連接，而且用戶端可以存取 Internet 並已登入公司區域網路時，您可以設定複寫，就好像遠端用戶端是直接在 LAN (區域網路) 一樣。 基於安全因素，可以讓不同的網路資源供透過 VPN 連接的使用者，以及供直接連接到 LAN (區域網路) 的使用者存取。  
  
 如需有關設定 VPN 的詳細資訊，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 文件集。  
  
## <a name="see-also"></a>另請參閱  
 [透過網際網路的複寫](replication-over-the-internet.md)  
  
  
