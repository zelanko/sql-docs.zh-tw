---
title: 升級 SQL Server 容錯移轉叢集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading failover clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], upgrading
ms.assetid: daac41fe-7d0b-4f14-84c2-62952ad8cbfa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a7a8d5f04808582bd56c106adce0df2c1f66aa77
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62913692"
---
# <a name="upgrade-a-sql-server-failover-cluster"></a>升級 SQL Server 容錯移轉叢集
  
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援在所有容錯移轉叢集節點上，個別從 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]、[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]、[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 與 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 容錯移轉叢集，升級 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 及 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]。  
  
 支援詳細資料如下：  
  
-   目前支援從使用者介面和命令提示字元進行升級。 如需詳細資訊，請參閱[升級 SQL Server 容錯移轉叢集執行個體 &#40;安裝程式&#41;](upgrade-a-sql-server-failover-cluster-instance-setup.md) 和[從命令提示字元安裝 SQL Server 2014](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)。  
  
-   從[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]升級-您可以在每個容錯移轉叢集節點上，從命令提示字元執行升級，或使用安裝程式 UI 來升級每個叢集節點。 如果全文檢索搜尋和複寫功能不存在升級的執行個體上，系統就會自動安裝它們，而不會提供省略它們的選項。  
  
-   Service Pack 安裝 - 您必須將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Service Pack 和修補程式個別套用至所有節點上的 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 容錯移轉叢集。  
  
-   不支援下列狀況：  
  
    -   您無法從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的獨立執行個體移轉至容錯移轉叢集。  
  
    -   將功能加入至容錯移轉叢集。 例如，您無法將 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 加入至現有的僅限 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]容錯移轉叢集。  
  
    -   您無法將容錯移轉叢集節點降級為獨立執行個體。  
  
-   如需詳細資訊，請參閱 [AlwaysOn 容錯移轉叢集執行個體 (SQL Server)](always-on-failover-cluster-instances-sql-server.md)。  
  
## <a name="upgrading-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster"></a>升級 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 多重子網路容錯移轉叢集  
 您無法將非多重子網[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]容錯移轉叢集直接升級為[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]多重子網容錯移轉叢集。 如需詳細資訊，請參閱[升級 SQL Server 容錯移轉叢集執行個體 &#40;安裝程式&#41;](upgrade-a-sql-server-failover-cluster-instance-setup.md)。  
  
## <a name="see-also"></a>另請參閱  
 [支援的版本與版本升級](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [升級 SQL Server 容錯移轉叢集實例 &#40;安裝程式&#41;](upgrade-a-sql-server-failover-cluster-instance-setup.md)   
 [Install SQL Server 2014 from the Command Prompt](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)  
  
  
