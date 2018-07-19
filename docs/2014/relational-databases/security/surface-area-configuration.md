---
title: 介面區組態 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- reducing attackable surface area
- upgrading SQL Server, security
- surface area configuration [SQL Server]
- surface area configuration [SQL Server], about surface area configuration
- attackable surface area [SQL Server]
- installing SQL Server, security
ms.assetid: f741169c-1453-4ad2-830b-bf2be27d712f
caps.latest.revision: 79
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7032966cb0fb1975b65847ac1e6e0a6c5dc43b1d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37172189"
---
# <a name="surface-area-configuration"></a>介面區組態
  在新安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]預設組態中，許多功能都不會啟用。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 為了將可能會遭受惡意使用者攻擊的功能數目最小化，因此會選擇性地只安裝與啟動主要的服務與功能。 系統管理員可在安裝期間變更這些預設值，也可以選擇性地啟用或停用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之執行中執行個體的功能。 此外，從其他電腦連接時，某些元件可能要等到設定通訊協定之後才能使用。  
  
> [!NOTE]  
>  與新安裝不同的是，在升級處理期間不會關閉任何現有的服務或功能，但是在升級完成後可能會套用其他介面區組態選項。  
  
## <a name="protocols-connection-and-startup-options"></a>通訊協定、連接和啟動選項  
 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員來啟動和停止服務、設定啟動選項，以及啟用通訊協定和其他連線選項。  
  
#### <a name="to-start-sql-server-configuration-manager"></a>啟動 SQL Server 組態管理員  
  
1.  指向 **[開始]** 功能表上的 **[所有程式]**，然後依序指向 [ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]] 和 **[組態工具]**，再按一下 **[SQL Server 組態管理員]**。  
  
    -   使用 **SQL Server 服務** 區域來啟動元件並設定自動啟動選項。  
  
    -   使用 **SQL Server 網路組態** 區域來啟用連線通訊協定，以及連線選項，例如固定 TCP/IP 通訊埠或強制加密。  
  
 如需詳細資訊，請參閱 [SQL Server 組態管理員](../sql-server-configuration-manager.md)。 遠端連接可能也會取決於防火牆的正確組態。 如需詳細資訊，請參閱 [設定 Windows 防火牆以允許 SQL Server 存取](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
## <a name="enabling-and-disabling-features"></a>啟用和停用功能  
 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 Facet 來設定啟用和停用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]功能。  
  
#### <a name="to-configure-surface-area-using-facets"></a>使用 Facet 來設定介面區  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的元件。  
  
2.  在 [物件總管] 中，以滑鼠右鍵按一下伺服器，然後按一下 [Facets]。  
  
3.  在 [檢視 Facets] 對話方塊中，展開 [Facet] 清單，並選取適當的 [介面區組態] Facet ([介面區組態]、[Analysis Services 的介面區組態]，或 [Reporting Services 介面區組態])。  
  
4.  在 **Facet 屬性**區域中，選取您想要用於每個屬性的值。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 若要定期檢查 Facet 的組態，請使用以原則為基礎的管理。 如需原則式管理的詳細資訊，請參閱 [使用原則式管理來管理伺服器](../policy-based-management/administer-servers-by-using-policy-based-management.md)。  
  
 您也可以使用 `sp_configure` 預存程序來設定 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 選項。 如需詳細資訊，請參閱 [伺服器設定選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)伺服器組態選項。  
  
 變更 [!INCLUDE[ssRS](../../includes/ssrs-md.md)] 的 **EnableIntegrated Security** 屬性時，請使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的屬性設定。 若要變更 [排程事件和報表傳遞] 屬性以及 [Web 服務和 HTTP 存取] 屬性時，請編輯 **RSReportServer.config** 組態檔。  
  
## <a name="command-prompt-options"></a>命令提示字元選項  
 您可以使用 **Invoke-PolicyEvaluation**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell Cmdlet 以叫用介面區組態原則。 如需詳細資訊，請參閱 [使用 Database Engine Cmdlet](../../database-engine/use-the-database-engine-cmdlets.md)。  
  
## <a name="soap-and-service-broker-endpoints"></a>SOAP 和 Service Broker 端點  
 若要關閉端點，請使用以原則為基礎的管理。 建立和改變端點的屬性時，請使用 [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql) 和 [ALTER ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql)。  
  
## <a name="related-content"></a>相關內容  
 [SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心](security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
