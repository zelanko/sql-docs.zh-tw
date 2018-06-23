---
title: 報表管理員 URL （SSRS 原生模式） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rsconfigtool.reportmanagervirtualdirectory.f1
ms.assetid: 45768952-23a6-45a5-b541-e7bf192b4a78
caps.latest.revision: 7
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 1469d877b992638119ad60bafadc1023a4ed5fc7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031354"
---
# <a name="report-manager-url-ssrs-native-mode"></a>報表管理員 URL (SSRS 原生模式)
  使用 [報表管理員 URL] 頁面可設定或修改用於存取報表管理員的 URL。 根據預設，報表管理員 URL 會繼承報表伺服器 Web 服務 URL 的前置詞、IP 位址和通訊埠。 這是因為報表管理員會提供在相同報表伺服器服務內執行之 Web 服務的前端存取權。 如果您要隔離服務應用程式並使用報表管理員來存取不同電腦上的報表伺服器 Web 服務，您必須編輯 RSReportServer.config 檔案，讓報表管理員指向不同的執行個體。 如需設定報表管理員連接到遠端報表伺服器的詳細資訊，請參閱[Reporting Services 組態管理員&#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式。  
  
 如果您設定報表伺服器在 SharePoint 整合模式下執行，請不要建立報表管理員 URL。 以 SharePoint 整合模式執行的報表伺服器不支援報表管理員。 如果報表管理員已經有 URL 存在，當您設定報表伺服器在 SharePoint 整合模式下執行之後，此 URL 將會變成無法使用。  
  
 若要開啟此頁面，請啟動[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]組態管理員，並按一下**報表管理員 URL**瀏覽窗格中。 如需如何啟動 Configuration Manager 的詳細資訊，請參閱[Reporting Services 組態管理員&#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
> [!NOTE]  
>  如果報表管理員尚未啟用，您就無法設定此頁面上的選項。 如需有關啟用報表管理員的詳細資訊，請參閱[Reporting Services 組態管理員&#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
## <a name="options"></a>選項。  
 **虛擬目錄**  
 為報表管理員指定虛擬目錄名稱。 相同電腦上的每一個報表管理員執行個體只能有一個虛擬目錄名稱。  
  
 **Url**  
 顯示為目前報表管理員執行個體定義的 URL。  
  
 **進階**  
 為目前報表管理員執行個體加入額外的 URL。  
  
## <a name="see-also"></a>另請參閱  
 [設定 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [組態檔中的 Url &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)   
 [設定報表伺服器 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  