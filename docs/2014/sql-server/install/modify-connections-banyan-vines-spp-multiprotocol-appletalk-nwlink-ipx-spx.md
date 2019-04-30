---
title: 修改使用 Banyan VINES Sequenced Packet Protocol (SPP)、 多重通訊協定、 AppleTalk 或 NWLink IPX SPX 網路通訊協定的連接 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- network protocols [SQL Server], modifying connections
- SPP [SQL Server]
- NWLink IPX/SPX [SQL Server]
- connections [SQL Server]
- AppleTalk [SQL Server]
- Sequenced Packet Protocol [SQL Server]
- Multiprotocol Net-Library [SQL Server]
- Banyan VINES Sequenced Package Protocol [SQL Server]
- IPX/SPX [SQL Server]
- protocols [SQL Server], modifying connections
- RPC [SQL Server]
ms.assetid: 5c5ae453-cc5b-4898-95c7-ad34157b1f60
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0cb9d235a02414b589735e7118bfe22f408d1d54
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199970"
---
# <a name="modify-connections-that-use-banyan-vines-sequenced-packet-protocol-spp-multiprotocol-appletalk-or-nwlink-ipx-spx-network-protocols"></a>修改使用 Banyan VINES Sequenced Packet Protocol (SPP)、多重通訊協定、AppleTalk 或 NWLink IPX SPX 網路通訊協定的連線
  Upgrade Advisor 偵測到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中不支援的用戶端伺服器連接通訊協定。 使用 Banyan VINES Sequenced Packet Protocol (SPP)、多重通訊協定 (RPC)、AppleTalk 與 NWLink IPX/SPX 網路通訊協定的用戶端應用程式必須使用支援的通訊協定進行連接。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 不支援 Banyan VINES Sequenced Packet Protocol (SPP)、多重通訊協定、AppleTalk 或 NWLink IPX/SPX 網路通訊協定。 先前使用這些通訊協定進行連接的用戶端必須選取不同的通訊協定。  
  
## <a name="corrective-action"></a>更正動作  
 變更用戶端應用程式，以便在連接至伺服器時使用支援的通訊協定。 如果您有使用了其中一個不支援之通訊協定的別名設定，則必須將別名修改為使用其中一個支援的通訊協定。  
  
 如果您的應用程式連接字串，特別使用或載入其中一種通訊協定，由其中一個指定的網路 = DBMSRPCN rpc，網路 = DBMSADSN Appletalk 或網路 = DBMSVINN Banyan VINES 屬性，或使用明確的前置詞，如"spx:*伺服器 \ 執行個體*"SPX，如"bv:*伺服器*」 針對 Banyan VINES，"adsp:*server*"appletalk，或"rpc:*server*"for多重通訊協定，然後您必須修改您的應用程式使用其中一個支援的通訊協定。  
  
 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜選擇網路通訊協定＞。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
