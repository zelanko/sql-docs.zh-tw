---
title: 修改使用 Banyan VINES 排序封包通訊協定（SPP）、多重通訊協定、AppleTalk 或 NWLink IPX SPX 網路通訊協定的連接 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
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
ms.openlocfilehash: cdbcaa39e3d9630bd4ea50919f31cdbb15a36d14
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66093903"
---
# <a name="modify-connections-that-use-banyan-vines-sequenced-packet-protocol-spp-multiprotocol-appletalk-or-nwlink-ipx-spx-network-protocols"></a>修改使用 Banyan VINES Sequenced Packet Protocol (SPP)、多重通訊協定、AppleTalk 或 NWLink IPX SPX 網路通訊協定的連線
  Upgrade Advisor 偵測到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中不支援的用戶端伺服器連接通訊協定。 使用 Banyan VINES Sequenced Packet Protocol (SPP)、多重通訊協定 (RPC)、AppleTalk 與 NWLink IPX/SPX 網路通訊協定的用戶端應用程式必須使用支援的通訊協定進行連接。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 不支援 Banyan VINES Sequenced Packet Protocol (SPP)、多重通訊協定、AppleTalk 或 NWLink IPX/SPX 網路通訊協定。 先前使用這些通訊協定進行連接的用戶端必須選取不同的通訊協定。  
  
## <a name="corrective-action"></a>更正動作  
 變更用戶端應用程式，以便在連接至伺服器時使用支援的通訊協定。 如果您有使用了其中一個不支援之通訊協定的別名設定，則必須將別名修改為使用其中一個支援的通訊協定。  
  
 如果您的應用程式連接字串特別使用或載入其中一個通訊協定，請指定 NETWORK = DBMSRPCN for RPC，NETWORK = DBMSADSN for Appletalk 或 NETWORK = DBMSVINN for Banyan VINES 屬性，或使用明確的前置詞，例如 "spx：*server\instance*" 代表 spx、"bv：*Server*" 代表 Banyan VINES、"adsp：*server*" 代表 appletalk，或 "RPC：*server*" 代表通訊協定，您必須將應用程式修改為使用其中一種支援的通訊協定。  
  
 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜選擇網路通訊協定＞。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
