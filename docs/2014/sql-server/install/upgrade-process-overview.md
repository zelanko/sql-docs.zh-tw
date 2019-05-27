---
title: 升級程序概觀 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- upgrading SQL Server
- Upgrade Advisor [SQL Server], process description
- SQL Server Upgrade Advisor, process description
- upgrade process [Upgrade Advisor]
ms.assetid: f77ffbab-a195-4124-acce-9c538f7ca9ce
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fb4bfb2073427d0f48b3d4a7ac7b7ab496299030
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66091514"
---
# <a name="upgrade-process-overview"></a>升級程序概觀
  本主題會提供 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Upgrade Advisor 的最佳作法資訊，以及升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 之建議程序的摘要。  
  
## <a name="upgrade-process"></a>升級程序  
 執行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 的伺服器可以升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 有些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件可以就地升級、有些元件必須移轉，而其他元件則已由新元件取代。 例如，從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) 便取代了 Data Transformation Services (DTS)，而且 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 不再支援 DTS。 當設計升級計畫時，您可能需要規劃將目前 DTS 封裝升級為 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝。  
  
 Upgrade Advisor 可讓您評估目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝、元件和相關檔案，以便識別在升級或移轉至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 期間或之後將導致問題發生的已知問題。 其中少數已知問題會封鎖 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 升級。 在 Upgrade Advisor 報表中，這些問題會識別為「升級封鎖程式」。 如果您在執行安裝程式之前沒有處理這些「升級封鎖程式」，[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝程式會結束，並建議您執行 Upgrade Advisor 來識別封鎖升級的特定問題。  
  
 建議的最佳作法是，在升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 之前，備份資料和系統設定，然後採取針對組織所定義之作業指導方針所述的策略性步驟。 請使用下列步驟來完成升級：  
  
1.  檢閱 [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)。  
  
2.  備份資料和系統設定。  
  
3.  執行 Upgrade Advisor。  
  
     Upgrade Advisor 不會修改資料或變更電腦的設定。  
  
4.  檢閱 Upgrade Advisor 報表中識別的問題。  
  
5.  解決讓您無法升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的任何封鎖問題。  
  
6.  解決任何其他升級前問題。  
  
7.  執行 Upgrade Advisor 來確認所有已知問題都已經解決。  
  
8.  執行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝程式。  
  
9. 解決任何升級後和移轉問題。  
  
## <a name="see-also"></a>另請參閱  
 [執行 Upgrade Advisor&#40;使用者介面&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)   
 [使用報表](../../../2014/sql-server/install/using-reports.md)   
 [使用升級建議程式](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
