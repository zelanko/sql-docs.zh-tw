---
title: "保護透過網際網路的複寫 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "安全性 [SQL Server 複寫], 網際網路"
  - "網際網路 [SQL Server 複寫], 安全性"
ms.assetid: 25b7af05-2721-4b24-9083-fb671e8bf4e0
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# 保護透過網際網路的複寫
  網際網路複寫可以提供彈性，特別是對於行動訂閱者，但是您必須正確設定網際網路複寫以保證充分的安全性。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 建議使用下列兩個透過網際網路安全共用資訊的技術之一：  
  
-   虛擬私人網路 (VPN)  
  
-   合併式複寫的 Web 同步處理選項  
  
## 虛擬私人網路  
 虛擬私人網路會提供一個簡單又安全的分層方式，透過網際網路複寫 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料。 透過網際網路的 VPN 連接在邏輯上的操作類似站台之間的「廣域網路」(WAN) 連結。  
  
 這藉由讓使用者能夠透過網際網路或其他公用網路，例如使用的通訊協定通道 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 點對點通道通訊協定 (PPTP) 適用於 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows NT 4.0 版或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 2000 作業系統或二層通道通訊協定 (L2TP) 適用於 Windows 2000 作業系統。 這個處理所提供的安全性和功能與私人網路中所提供的類似。  
  
 如需有關設定 VPN 的詳細資訊，請參閱 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 文件集。  
  
## 透過 IIS 的 Web 同步處理  
 用於合併式複寫的 Web 同步處理選項提供了經由使用 HTTPS 通訊協定來複寫資料的功能，這是一個透過防火牆來複寫資料的便利方式。 如需詳細資訊，請參閱 [設定 Web 同步處理](../../../relational-databases/replication/configure-web-synchronization.md) 和 [Web 同步處理的安全性架構](../../../relational-databases/replication/security/security-architecture-for-web-synchronization.md)。  
  
## 另請參閱  
 [複寫安全性最佳做法](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [安全性和保護 & #40。複寫 & #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  