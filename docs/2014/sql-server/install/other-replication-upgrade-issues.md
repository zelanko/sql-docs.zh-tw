---
title: 其他複寫升級問題 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- system tables [SQL Server], replication
- passwords [SQL Server replication]
- versions [SQL Server replication]
- connections [SQL Server replication]
- scripts [SQL Server replication]
- ActiveX controls [SQL Server replication]
ms.assetid: 8a5e74be-4992-4f17-b20c-c3dce8f49329
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e5ffde063d94f0e08ea0e82e6b5998a6d23cfaac
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200728"
---
# <a name="other-replication-upgrade-issues"></a>其他複寫升級問題
  本主題涵蓋 Upgrade Advisor 未報告的一些升級問題。  
  
## <a name="versions-supported"></a>支援的版本  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支援從舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級複寫的資料庫。 當節點正在升級時，您不必停止其他節點上的活動。 請務必遵守有關拓撲中支援之版本的規則。  
  
 當您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的不同版本之間複寫時，通常受限於所使用之最舊版本的功能。  
  
> [!NOTE]  
>  由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 磁碟儲存格式在 64 位元和 32 位元的環境中是相同的，所以複寫拓撲可結合在 32 位元環境中執行的伺服器執行個體，以及在 64 位元環境中執行的伺服器執行個體。  
  
 對於所有複寫類型而言，散發者的版本都不能比發行者的版本還舊  (通常散發者和發行者會是相同的執行個體)。  
  
 如果是異動複寫，交易式發行集的訂閱者可以是兩個發行者版本的其中任何版本。  
  
 如果是合併式複寫，合併式發行集的訂閱者版本可以是任何不晚於發行者的版本。  
  
## <a name="merge-replication-batches-changes"></a>合併式複寫的批次變更  
 合併代理程式所進行的變更會批次處理以增進效能；因此，可在單一陳述式內插入、更新或刪除多個資料列。 如果發行集或訂閱資料庫中的任何已發行的資料表有觸發程序，請確定這些觸發程序可以處理多資料列插入、更新及刪除。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜DML 觸發程序的多重資料列考量＞。  
  
## <a name="activex-control-changes"></a>ActiveX 控制項變更  
 下列是已經對複寫 ActiveX 控制項所做的變更：  
  
-   所有 ActiveX 控制項在撰寫指令碼和初始化時都標示為不安全。  
  
-   快照集 ActiveX 控制項已經卸除。 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或透過複寫預存程序來以程式設計的方式建立及管理快照集。 如需詳細資訊，請參閱《[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 線上叢書》中的＜如何：建立和套用初始快照集 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])＞和＜如何：建立初始快照集 (複寫 Transact-SQL 程式設計)＞主題。  
  
-   散發 ActiveX 控制項和合併 ActiveX 控制項已被取代。 將會使用 Replication Management Objects (RMO) 來針對 Managed 程式碼應用程式提供類似的功能。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜同步處理訂閱 (RMO 程式設計)＞。  
  
## <a name="see-also"></a>另請參閱  
 [複寫升級問題](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
  
