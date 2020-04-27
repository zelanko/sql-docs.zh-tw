---
title: 電子郵件設定-Configuration Manager （SSRS 原生模式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.rsconfigtool.emailsettings.f1
helpviewer_keywords:
- SQL11.rsconfigtool.emailsettings.F1
ms.assetid: cdad1529-bfa6-41fb-9863-d9ff1b802577
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 808ad67429ee49d6b04533863112b4cbb3af2514
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108880"
---
# <a name="e-mail-settings---configuration-manager-ssrs-native-mode"></a>電子郵件設定 - 組態管理員 (SSRS 原生模式)
  使用此頁面，即可指定會啟用從報表伺服器傳遞報表伺服器電子郵件的 Simple Mail Transport Protocol (SMTP) 設定。 您可以使用報表伺服器電子郵件傳遞延伸模組，透過電子郵件訂閱來散發報表或報表處理通知。 報表伺服器電子郵件傳遞延伸模組，需要使用 [從:] 欄位中的 SMTP 伺服器和電子郵件地址。  
  
 其他組態設定可用來進一步自訂電子郵件訂閱，其中包含會限制郵件伺服器主機和轉譯延伸模組之可用性的設定。 您無法在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員中指定這些設定。 若要設定其他設定，則您必須手動編輯 RSReportServer.config 檔案。 如需詳細資訊，請參閱《線上叢書》中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的[設定報表伺服器的電子郵件傳遞 &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)和[Reporting Services 設定檔](../report-server/reporting-services-configuration-files.md)案。  
  
 若要開啟此頁面，請啟動 Reporting Services 組態管理員，然後按一下流覽窗格中的 [**電子郵件設定**]。 如需詳細資訊，請參閱 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]原生模式。  
  
## <a name="options"></a>選項。  
 **寄件者位址**  
 指定用於所產生電子郵件之 [從:] 欄位中的電子郵件地址。 您必須指定有權從 SMTP 伺服器傳送郵件的使用者帳戶。  
  
 **目前的 SMTP 傳遞方法**  
 指定報表伺服器電子郵件是透過 SMTP 伺服器來傳送。 這是在 Reporting Services 組態管理員中，您唯一可以指定的傳遞方法。  
  
 替代的傳遞方法是使用本機 SMTP 服務收取目錄。 如果無法使用網路 SMTP 服務，您就可以使用此傳遞方法。 若要指定本機 SMTP 服務收取目錄，您必須編輯 RSReportServer.config 檔案。 如果您編輯設定檔以使用本機 SMTP 服務收取目錄，Reporting Services 組態管理員會將 [**傳遞方法**] 選項設定為 [*自訂*]，以指出傳遞方法是在設定檔中指定。  
  
 在組態檔中，傳遞方法是透過 `SendUsing` 組態設定來加以設定。 如需有關指定`SendUsing`設定的詳細資訊，請參閱[為電子郵件傳遞設定報表伺服器 &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)。  
  
 **SMTP 伺服器**  
 指定要使用的 SMTP 伺服器或閘道。 您可以在網路上使用本機伺服器或 SMTP 伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [針對 &#40;SSRS Configuration Manager 的電子郵件傳遞設定報表伺服器&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)   
 [Reporting Services 組態管理員 &#40;SSRS 原生模式的 F1 說明主題&#41;](../../sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)  
  
  
