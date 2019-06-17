---
title: 保護透過網際網路的複寫 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server replication], Internet
- Internet [SQL Server replication], security
ms.assetid: 25b7af05-2721-4b24-9083-fb671e8bf4e0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 78dfc544d7fd01f6641df6c0968d4a59a668cdd3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62960032"
---
# <a name="securing-replication-over-the-internet"></a>Securing Replication Over the Internet
  網際網路複寫可以提供彈性，特別是對於行動訂閱者，但是您必須正確設定網際網路複寫以保證充分的安全性。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 建議使用下列兩個透過網際網路安全共用資訊的技術之一：  
  
-   虛擬私人網路 (VPN)  
  
-   合併式複寫的 Web 同步處理選項  
  
## <a name="virtual-private-network"></a>虛擬私人網路  
 虛擬私人網路會提供一個簡單又安全的分層方式，透過網際網路複寫 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料。 透過網際網路的 VPN 連接在邏輯上的操作類似站台之間的「廣域網路」(WAN) 連結。  
  
 藉由允許使用者穿過網際網路或其他公用網路 (使用如 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows NT 4.0 版本或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows2000 作業系統可用的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Point-to-Point Tunneling Protocol (PPTP) 之類的通訊協定，或 Windows 2000 作業系統可用的 Layer Two Tunneling Protocol (L2TP)) 的通道即可達成。 這個處理所提供的安全性和功能與私人網路中所提供的類似。  
  
 如需有關設定 VPN 的詳細資訊，請參閱 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 文件集。  
  
## <a name="web-synchronization-through-iis"></a>透過 IIS 的 Web 同步處理  
 用於合併式複寫的 Web 同步處理選項提供了經由使用 HTTPS 通訊協定來複寫資料的功能，這是一個透過防火牆來複寫資料的便利方式。 如需詳細資訊，請參閱[設定 Web 同步處理](../configure-web-synchronization.md)和 [Web 同步處理的安全性架構](security-architecture-for-web-synchronization.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [SQL Server 複寫安全性](view-and-modify-replication-security-settings.md)  
  
  
