---
title: 設定管理概念的 WMI 提供者 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management
- SQL Server WMI Provider
- configuration management [WMI]
- WMI Provider for Configuration Management, about WMI Provider for Configuration Management
ms.assetid: 7e41db24-b915-4eb8-a1d6-e6948ee915b7
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: ac064258da9ae55039c350f50d153d0c60323621
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211627"
---
# <a name="wmi-provider-for-configuration-management-concepts"></a>組態管理的 WMI 提供者概念
  WMI 提供者是一種已發行的層，可[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]搭配[!INCLUDE[msCoName](../../includes/msconame-md.md)]管理主控台（MMC）和[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager 的 Configuration Manager 嵌入式管理單元使用。 它會提供統一的方式來協助您連結管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員所要求之登錄作業的 API 呼叫，並在選取的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務上，提供增強的控制和操作功能。  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WMI 提供者是一個 DLL 和 MOF 檔案，會透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式自動編譯。  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WMI 提供者包含一組物件類別，用於透過下列方法控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務：  
  
-   可在其中內嵌 Windows 查詢語言 (WQL) 的指令碼語言，例如，VBScript、[!INCLUDE[jsprjscript](../../includes/jsprjscript-md.md)] 或 Perl。  
  
-   SMO Managed 程式碼程式中的 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 物件。  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員或包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WMI 提供者嵌入式管理單元的 MMC。  
  
## <a name="using-a-script-language"></a>使用指令碼語言  
 使用指令碼語言的優點包括：  
  
-   不需要開發環境。  
  
-   支援指令碼語言的檔案隨處可得。  
  
 除了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WMI 提供者之外，指令碼也可以使用其他 WMI 提供者。 網域管理員可以使用指令碼，在網路內的多部電腦上設定服務、網路設定以及別名設定。  
  
 本節以更詳細的方式處理從指令碼存取組態管理的 WMI 提供者。  
  
## <a name="using-the-smo-managedcomputer-object"></a>使用 SMO ManagedCompute 物件  
 
  <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 物件是一個 Managed SMO 物件，可存取組態管裡的 WMI 提供者。 透過使用 SMO 程式，<xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 物件可用於檢視與修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務、網路設定以及別名設定。 如需詳細資訊，請參閱[使用 WMI 提供者管理服務和網路設定](../server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md)。  
  
## <a name="using-the-microsoft-management-console-or-sql-server-configuration-manager"></a>使用 Microsoft Management Console 或 SQL Server 組態管理員  
 Microsoft Management Console (MMC) 提供一個管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務 (而非指令碼語言或 Managed 程式碼程式) 的介面。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management MMC 嵌入式管理單元可用於停止和啟動服務，以及變更服務帳戶。  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員也可用於管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務、用戶端與伺服器通訊協定，以及伺服器別名  
  
## <a name="see-also"></a>另請參閱  
 [瞭解設定管理的 WMI 提供者](understanding-the-wmi-provider-for-configuration-management.md)   
 [使用 WMI 提供者進行設定管理](working-with-the-wmi-provider-for-configuration-management.md)   
 [搭配組態管理的 WMI 提供者使用 WQL 與指令碼語言](using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
