---
title: 報表伺服器命令提示字元公用程式 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsconfig utility
- components [Reporting Services], command line utilities
- rs utility
- command prompt utilities [Reporting Services]
- rskeymgmt utility
ms.assetid: 68f2f9f4-f894-40ff-a71c-f9756bf4b68c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 07da79ea46ca0e9e23abb7197730821d8c31bfa8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66099996"
---
# <a name="report-server-command-prompt-utilities-ssrs"></a>報表伺服器命令提示字元公用程式 (SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包括您可以用來管理報表伺服器的數個命令列公用程式。 這些公用程式會在您安裝報表伺服器時自動安裝。  
  
|名稱|命令檔|支援的部署模式|描述|  
|----------|------------------|-------------------------------|-----------------|  
|RSS 公用程式|rs.exe|原生模式和 SharePoint 模式。 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版本導入了 SharePoint 模式的支援。|[rs 公用程式](rs-exe-utility-ssrs.md) 是一個 Script Host，您可以使用它來執行編寫指令碼的作業。 使用此工具即可執行 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 指令碼，於報表伺服器資料庫間複製資料、發行報表、在報表伺服器資料庫中建立項目等等。 若要深入了解使用指令碼來管理伺服器，請參閱 [編寫部署和管理工作的指令碼](script-deployment-and-administrative-tasks.md)。|  
|PowerShell 指令程式||僅 SharePoint|如需 PowerShell Cmdlet 的清單，請參閱 [Reporting Services SharePoint 模式的 PowerShell Cmdlet](../powershell-cmdlets-for-reporting-services-sharepoint-mode.md)。|  
|rsconfig 公用程式|rsconfig.exe|僅原生|[rsconfig 公用程式](rsconfig-utility-ssrs.md) 用於設定和管理至報表伺服器資料庫的報表伺服器連接。 您也可以使用它來指定自動執行報表處理所使用的使用者帳戶。 如需詳細資訊，請參閱 [Reporting Services 報表伺服器 &#40;原生模式&#41;](../report-server/reporting-services-report-server-native-mode.md)。 若要深入了解連線設定，請參閱[設定報表伺服器資料庫連線 &#40;SSRS 設定管理員&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。|  
|Rskeymgmt 公用程式|rskeymgmt.exe|僅原生|[rskeymgmt 公用程式](rskeymgmt-utility-ssrs.md) 是一個加密金鑰管理工具。 您可以利用它來備份、套用、重新建立及刪除對稱金鑰。 您也可以使用此工具，將報表伺服器執行個體附加至共用的報表伺服器資料庫。 Rskeymgmt 可以在資料庫復原作業中使用。 您可以套用對稱金鑰的備份副本，在新安裝中重複使用現有的資料庫。 如果無法復原金鑰，此工具可刪除不再使用的加密內容。 若要深入了解金鑰管理和敏感性資料儲存，請參閱[儲存加密的報表伺服器資料 &#40;SSRS 設定管理員&#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md) 和[設定和管理加密金鑰 &#40;SSRS 設定管理員&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md)。|  
  
> [!NOTE]  
>  如果您習慣使用有圖形化使用者介面的工具，可以使用 Reporting Services 組態管理員，而不要使用 `rsconfig` 和 `rskeymgmt`。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Reporting Services 工具](reporting-services-tools.md)   
 [Reporting Services 報表伺服器 &#40;原生模式&#41;](../report-server/reporting-services-report-server-native-mode.md)  
  
  
