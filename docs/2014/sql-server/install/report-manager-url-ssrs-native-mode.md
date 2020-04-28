---
title: 報表管理員 URL （SSRS 原生模式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.rsconfigtool.reportmanagervirtualdirectory.f1
ms.assetid: 45768952-23a6-45a5-b541-e7bf192b4a78
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: dd4ff661a10eca71781aee9d1886e80936f6246d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952416"
---
# <a name="report-manager-url-ssrs-native-mode"></a>報表管理員 URL (SSRS 原生模式)
  使用 [報表管理員 URL] 頁面可設定或修改用於存取報表管理員的 URL。 根據預設，報表管理員 URL 會繼承報表伺服器 Web 服務 URL 的前置詞、IP 位址和通訊埠。 這是因為報表管理員會提供在相同報表伺服器服務內執行之 Web 服務的前端存取權。 如果您要隔離服務應用程式並使用報表管理員來存取不同電腦上的報表伺服器 Web 服務，您必須編輯 RSReportServer.config 檔案，讓報表管理員指向不同的執行個體。 如需設定報表管理員連接到遠端報表伺服器的詳細資訊，請參閱[Reporting Services 組態管理員 &#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]原生模式。  
  
 如果您設定報表伺服器在 SharePoint 整合模式下執行，請不要建立報表管理員 URL。 以 SharePoint 整合模式執行的報表伺服器不支援報表管理員。 如果報表管理員已經有 URL 存在，當您設定報表伺服器在 SharePoint 整合模式下執行之後，此 URL 將會變成無法使用。  
  
 若要開啟此頁面，請啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員，並按一下導覽窗格中的 **[報表管理員 URL]** 。 如需如何啟動 Configuration Manager 的詳細資訊，請參閱[Reporting Services 組態管理員 &#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
> [!NOTE]  
>  如果報表管理員尚未啟用，您就無法設定此頁面上的選項。 如需啟用報表管理員的詳細資訊，請參閱[Reporting Services 組態管理員 &#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
## <a name="options"></a>選項  
 **虛擬目錄**  
 為報表管理員指定虛擬目錄名稱。 相同電腦上的每一個報表管理員執行個體只能有一個虛擬目錄名稱。  
  
 **URL**  
 顯示為目前報表管理員執行個體定義的 URL。  
  
 **進階**  
 為目前報表管理員執行個體加入額外的 URL。  
  
## <a name="see-also"></a>另請參閱  
 [設定 SSRS Configuration Manager &#40;的 URL&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [&#40;SSRS Configuration Manager 的設定檔中的 Url&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)   
 [設定報表伺服器 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
