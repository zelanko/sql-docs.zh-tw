---
title: 變更認證嚮導（SSRS 原生模式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.changecredentialswizard.F1
helpviewer_keywords:
- Change Credentials Wizard
- report server database, reconfigure
ms.assetid: 9eb4060a-9c3e-41e0-8767-3cfaebc45de7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 07ca904ab8f98dd4dcbdba3f18f4a6fc6469f26a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952322"
---
# <a name="change-credentials-wizard-ssrs-native-mode"></a>變更認證精靈 (SSRS 原生模式)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員提供了變更認證精靈，可引導您重新設定報表伺服器用來連接報表伺服器資料庫之帳戶的步驟。 當您變更認證時，組態管理員將會在報表伺服器目前使用之報表伺服器資料庫的資料庫伺服器上，更新所有的權限和資料庫登入資訊。  
  
 若要啟動此精靈，請按一下 **組態管理員內 [資料庫] 頁面上的** [變更認證] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。 如需如何啟動[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager 的指示，請參閱[Reporting Services 組態管理員 &#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]原生模式。  
  
## <a name="options"></a>選項  
 **資料庫伺服器**  
 指定執行報表伺服器資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]之實例的名稱。  
  
 若要連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，您必須使用有權登入伺服器及更新資料庫資訊的認證。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員會使用目前的 Windows 認證，但是如果您沒有登入或資料庫權限，您可以指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫登入。  
  
 您不能指定不同的 Windows 認證。 如果您想要以不同的 Windows 使用者身分連接，請以該使用者身分登入，然後啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員。  
  
 **認證**  
 指定用來將報表伺服器連接到報表伺服器資料庫的帳戶。 有效的值包括報表伺服器 Web 服務的服務帳戶、用來主控報表伺服器之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上定義的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 資料庫登入，或是 Windows 帳戶。 如果您使用 Windows 帳戶，如果報表伺服器和資料庫位於相同的電腦上，您可以指定本機帳戶（*\<computername>\\<\>* 使用者名稱），如果是在相同網域中的不同電腦上，則可指定網域使用者帳戶（*\<網域>\\<使用者名稱\>*）。  
  
 報表伺服器將會建立資料庫登入，並為您指定的帳戶指派資料庫權限。  
  
 報表伺服器不會建立帳戶本身。 您所指定的帳戶必須已經存在，而且對部署組態必須是有效的。 具體而言，如果資料庫位於遠端電腦上，而且您想要使用 Windows 帳戶，您就必須指定在該電腦上具有登入權限的帳戶。  
  
 如果此電腦位於不同的網域或不信任的網域中，請考慮使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫登入。 如需選擇帳戶的詳細資訊，請參閱[將報表伺服器資料庫連接設定 &#40;SSRS Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。  
  
 **摘要**  
 請在執行精靈之前先確認設定。  
  
 **進度和完成**  
 監視每項工作的進度。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫 &#40;SSRS 原生模式&#41;](../../../2014/sql-server/install/database-ssrs-native-mode.md)   
 [&#40;SSRS 原生模式的變更資料庫 Wizard&#41;](../../../2014/sql-server/install/change-database-wizard-ssrs-native-mode.md)   
 [建立原生模式報表伺服器資料庫 &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Reporting Services 組態管理員 &#40;SSRS 原生模式的 F1 說明主題&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [設定報表伺服器資料庫連接 &#40;SSRS 組態管理員&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  
