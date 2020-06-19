---
title: 選擇網路通訊協定 |Microsoft Docs
description: 比較和對比可用來連接到 SQL Server 資料庫引擎的網路通訊協定，例如共用記憶體、TCP/IP 和具名管道。
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- shared memory [SQL Server]
- Named Pipes [SQL Server]
- TCP [SQL Server]
- network protocols [SQL Server], choosing
- protocols [SQL Server], choosing
- NWLink IPX/SPX [SQL Server]
- client configuration [SQL Server], protocols
- VIA
- Multiprotocol Net-Library [SQL Server]
- IPX/SPX [SQL Server]
- Banyan VINES
- protocols [SQL Server], client configuration
ms.assetid: 6565fb7d-b076-4447-be90-e10d0dec359a
author: rothja
ms.author: jroth
ms.openlocfilehash: 20156e41bffcdca51ac8d1e16bcbff8d61079c73
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85008198"
---
# <a name="choosing-a-network-protocol"></a>選擇網路通訊協定
  若要連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，必須啟用網路通訊協定。 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以同時服務數個通訊協定上的要求。 用戶端會使用單一通訊協定連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果用戶端程式不知道 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在接聽哪個通訊協定，請設定用戶端循序嘗試多個通訊協定。 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員來啟用、停用及設定網路通訊協定。  
  
## <a name="shared-memory"></a>共用記憶體  
 共用記憶體是使用上最簡單的通訊協定，而且不用設定任何設定。 因為使用共用記憶體通訊協定的用戶端，只能連接到在相同電腦上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，所以不適用於大部分資料庫活動。 當您懷疑其他通訊協定的設定不正確時，請使用共用記憶體通訊協定進行疑難排解。  
  
> [!NOTE]  
>  使用 MDAC 2.8 或舊版的用戶端無法使用共用記憶體通訊協定。 即使這些使用者嘗試使用此通訊協定，還是會自動切換成具名管道通訊協定。  
  
## <a name="tcpip"></a>TCP/IP  
 TCP/IP 是網際網路廣泛使用的一般通訊協定。 其可在具有各種硬體架構與不同作業系統之電腦的互連網路間通訊。 TCP/IP 包括了路由網路傳輸量的標準，同時提供了進階安全性功能， 為現今企業中最常用的通訊協定。 設定電腦使用 TCP/IP 是一件很複雜的作業，但大部分網路電腦都已正確完成設定。 若要設定「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」中未公開的 TCP/IP 設定，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 文件集。  
  
## <a name="named-pipes"></a>具名管道  
 「具名管道」是為區域網路開發的通訊協定。 有一個處理序會使用部分記憶體將資訊傳遞給另一個處理序，如此該處理序的輸出會是另一個處理序的輸入。 第二個處理序可以在本機 (跟第一個處理序位於相同的電腦上) 或位於遠端 (在網路電腦上)。  
  
## <a name="named-pipes-vs-tcpip-sockets"></a>具名管道與TCP/IP 通訊端  
 在速度快的區域網路 (LAN) 環境中，傳輸控制通訊協定/網際網路通訊協定 (TCP/IP) 通訊端與具名管道用戶端在效能方面可相互媲美。 但是，若使用速度較慢的網路，例如，廣域網路 (WAN) 或撥號網路，TCP/IP 通訊端與具名管道用戶端之間，在效能上的差異就顯而易見。 這是因為跨處理序通訊 (IPC) 機制，在對等端之間通訊的方式不同。  
  
 對於具名管道，網路通訊一般較為互動。 對等會等到另一個對等使用讀取命令，要求傳送資料時才會傳送。 網路讀取動作在開始讀取資料之前，一般會涉及一連串的對等具名管道訊息。 這些在速度慢的網路中要付出的成本可能相當昂貴，而且會導致產生過多的網路傳輸量，而影響到其他網路用戶端。  
  
 釐清您正在討論的是本機管道或網路管道也很重要。 如果在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的電腦本機執行伺服器應用程式，則可以選擇本機的具名管道通訊協定。 本機的具名管道會在核心模式下執行且執行速度會相當快。  
  
 對於 TCP/IP 通訊端，資料傳輸較為簡化而且負擔較輕。 資料傳輸也可以得利於 TCP/IP 通訊端效能增強機制 (例如，視窗型、延遲的收條等等)， 這對速度慢的網路非常有幫助。 視應用程式類型而定，效能差異可能十分顯著。  
  
 TCP/IP 通訊端也支援積存佇列， 跟在嘗試連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時可能會導致管道忙碌而產生錯誤的具名管道相比，可提供一些緩衝效果。  
  
 一般來說，速度慢的 LAN、WAN 或撥接網路會偏好使用 TCP/IP，而當不用擔心網路速度時，具名管道會是較佳的選擇，因為提供的功能較多、操作更為簡單，而且組態選項較多。  
  
## <a name="enabling-the-protocol"></a>啟用通訊協定  
 用戶端與伺服器兩者必須都啟用通訊協定，才能夠運作。 伺服器可以同時接聽來自所有已啟用之通訊協定上的要求。 用戶端電腦可挑選一個通訊協定，或按 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員中列出的通訊協定依序嘗試。  
  
 如需如何設定通訊協定並連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的簡要教學課程，請參閱 [教學課程：Database Engine 使用者入門](../../relational-databases/tutorial-getting-started-with-the-database-engine.md)。  
  
  
