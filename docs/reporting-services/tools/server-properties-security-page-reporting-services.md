---
title: 伺服器屬性 (安全性頁面) - Reporting Services | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.serverproperties.security.f1
ms.assetid: f49aedc6-f145-4df1-8f69-d5d910f492c6
author: markingmyname
ms.author: maghan
ms.date: 06/10/2016
ms.openlocfilehash: 48fd1cf08882291515a0797957d9999f6bf67e90
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47738756"
---
# <a name="server-properties-security-page---reporting-services"></a>伺服器屬性 (安全性頁面) - Reporting Services

  使用 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 中的這個 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 頁面，即可關閉可能會危害報表伺服器的功能。 雖然關閉這些功能會限制某些功能，但是也可能會透過減少特定威脅，改善報表伺服器的整體安全性。  
  
 開啟此頁面：
 1) 啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。
 2) 連接到報表伺服器執行個體。
 3) 以滑鼠右鍵按一下報表伺服器名稱，然後選取 [屬性]。
 4) 按一下 [安全性]，即可開啟此頁面。  
  
## <a name="options"></a>選項。

### <a name="enable-windows-integrated-security-for-report-data-sources"></a>為報表資料來源啟用 Windows 整合式安全性

 指定報表資料來源的連線是否使用已要求報表之使用者的 Windows 安全性權杖。  
  
 如果您關閉這項功能，就無法使用報表資料來源屬性頁面中的 Windows 整合式安全性功能。 如果報表資料來源是針對 Windows 整合式安全性所設定，而且您之後關閉這項功能，則報表伺服器會立即更新所有資料來源連線屬性，以提示使用者輸入認證。  
  
### <a name="enable-ad-hoc-reporting"></a>啟用隨選報表

 指定使用者是否可以從報表產生器報表執行隨選查詢，而且當使用者按一下感興趣的資料時，系統就會自動產生新的報表。  
  
 設定這個選項可決定報表伺服器上的 **EnableLoadReportDefinition** 屬性設為 **True** 還是 **False**。 如果您清除此選項，則會將此屬性設定為 **False**，而且報表伺服器不會產生在資料瀏覽期間建立的點選連結報表。 所有 **LoadReportDefinition** 方法的呼叫都會遭到封鎖。  
  
 關閉此選項可減少惡意使用者利用 **LoadReportDefinition** 要求讓報表伺服器超過負載，藉以啟動阻斷服務攻擊的威脅。  
  
## <a name="see-also"></a>另請參閱

 [設定報表伺服器屬性 &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md) [連線至 Management Studio 中的報表伺服器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md) [指定報表資料來源的認證及連線資訊](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md) [Management Studio F1 說明中的報表伺服器](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)
