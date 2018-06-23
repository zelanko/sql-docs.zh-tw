---
title: Analysis Services 組態-帳戶提供 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Analysis Services configuration
- account provisioning
ms.assetid: 169b1af2-6fe2-467f-8ca4-919f24c620ce
caps.latest.revision: 28
author: HeidiSteen
ms.author: heidist
manager: jhubbard
ms.openlocfilehash: 4df78bd3cf29b2f767fafb1dcc5066a2e1d80a1f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146230"
---
# <a name="analysis-services-configuration---account-provisioning"></a>Analysis Services 組態 - 帳戶提供
  此用此頁面可以設定伺服器模式，以及將管理權限授與需要無限制存取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的使用者或服務。 安裝程式不會自動將本機 Windows 群組 BUILTIN\Administrators 加入您所安裝之執行個體的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器管理員角色。 如果您想要將本機 Administrators 群組加入至伺服器管理員角色，就必須明確指定該群組。  
  
 如果您要安裝 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]，請務必將管理權限授與負責在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服陣列中進行 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 部署的 SharePoint 伺服陣列管理員或服務管理員。 如需有關[!INCLUDE[ssGeminiMTS](../../includes/ssgeminimts-md.md)]安裝與服務帳戶需求，請參閱[與 SharePoint 安裝 SQL Server BI 功能&#40;PowerPivot 和 Reporting Services&#41;](../../../2014/sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)。  
  
## <a name="options"></a>選項。  
 **伺服器模式** - 伺服器模式指定可以部署到伺服器的 Analysis Services 資料庫類型。 伺服器模式是在安裝期間決定，之後不能修改。 每個模式是互斥的，也就是說，您需要兩個 Analysis Services 執行個體，各設定為不同的模式，以便同時支援傳統 OLAP 和表格式模型方案。  
  
 **指定管理員** - 您必須為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體至少指定一個伺服器管理員。 您所指定的使用者或群組將成為所安裝之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的伺服器管理員角色成員。 這些都必須是與安裝該軟體的電腦處於相同網域中的 Windows 網域使用者帳戶。  
  
> [!NOTE]  
>  使用者帳戶控制 (UAC) 為 Windows 安全性功能，會要求系統管理員明確地核准系統管理動作或應用程式，之後才會允許這些項目執行。 由於 UAC 預設為開啟，系統將會提示您允許需要更高權限的特定作業。 您可以設定 UAC，以變更預設行為或針對特定程式自訂 UAC。 如需 UAC 和 UAC 組態的詳細資訊，請參閱[使用者帳戶控制逐步指南](http://go.microsoft.com/fwlink/?linkid=196350)和[使用者帳戶控制 (Wikipedia)](http://go.microsoft.com/fwlink/?linkid=196351)。  
  
## <a name="see-also"></a>另請參閱  
 [設定服務帳戶&#40;Analysis Services&#41;](../../../2014/analysis-services/instances/configure-service-accounts-analysis-services.md)   
 [設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  