---
title: 移除 SQL Server 容錯移轉叢集執行個體 (安裝程式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- clusters [SQL Server], removing failover clustered instance
- failover clustering [SQL Server], removing failover clustered instance
- uninstalling failover clustered instances
- removing failover clustered instances
ms.assetid: bf63353b-69cf-4c5c-98ea-7b151e36537f
caps.latest.revision: 37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8bab3fe033857578977519f1893b80ae6c37cfef
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37251160"
---
# <a name="remove-a-sql-server-failover-cluster-instance-setup"></a>移除 SQL Server 容錯移轉叢集執行個體 (安裝程式)
  您可以使用這個程序來解除安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體。  
  
> [!IMPORTANT]  
>  若要更新或移除 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集，您必須是本機系統管理員，並且具有在容錯移轉叢集的所有節點上以服務登入的權限。  
  
 **開始之前**  
  
 在解除安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集之前，請先考慮下列重點：  
  
-   若意外解除安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資源將無法啟動。 若要重新安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client，請執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式以安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 必要元件。  
  
-   如果解除安裝具有一個以上 SQL IP 叢集資源的容錯移轉叢集，您必須使用叢集管理員移除其他 SQL IP 資源。  
  
 如需命令提示字元語法的詳細資訊，請參閱 <<c0> [ 從命令提示字元安裝 SQL Server 2014](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)。  
  
### <a name="to-uninstall-a-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>解除安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集  
  
1.  若要解除安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉叢集，請使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式所提供的「移除節點」功能來分別移除每個節點。 如需詳細資訊，請參閱[在 SQL Server 容錯移轉叢集中加入或移除節點 &#40;安裝程式&#41;](add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)。  
  
## <a name="see-also"></a>另請參閱  
 [檢視與讀取 SQL Server 安裝程式記錄檔](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
