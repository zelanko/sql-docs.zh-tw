---
title: 伺服器屬性 (安全性頁面) - Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.security.f1
ms.assetid: f49aedc6-f145-4df1-8f69-d5d910f492c6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a49f56c4e898b0189ce0f8bf5008873e13dc6223
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66099560"
---
# <a name="server-properties-security-page---reporting-services"></a>伺服器屬性 (安全性頁面) - Reporting Services
  您可以使用這個頁面來關閉可能會危害報表伺服器的功能。 雖然關閉這些功能會限制某些功能，但是也可能會透過減少特定威脅，改善報表伺服器的整體安全性。  
  
 若要開啟此頁面，請啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、連接至報表伺服器執行個體、以滑鼠右鍵按一下報表伺服器名稱，然後選取 [屬性]  。 按一下 [安全性]****，即可開啟此頁面。  
  
## <a name="options"></a>選項。  
 **為報表資料來源啟用 Windows 整合式安全性**  
 指定是否可以使用要求報表之使用者的 Windows 安全性 Token 來建立報表資料來源的連接。  
  
 如果您關閉這項功能，就無法使用報表資料來源屬性中的 Windows 整合式安全性功能。 如果報表資料來源是針對 Windows 整合式安全性所設定，而且您之後關閉了這項功能，則報表伺服器將立即更新所有資料來源連接屬性，以便提示使用者輸入認證。  
  
 **啟用特定報表**  
 指定使用者是否可以從報表產生器報表執行隨選查詢，而且當使用者按一下感興趣的資料時，系統就會自動產生新的報表。  
  
 設定這個選項會決定報表伺服器上的 `EnableLoadReportDefinition` 屬性設定為 `True` 或 `False`。 如果您清除此選項，這個屬性將會設定為 `False` 而且報表伺服器將不會產生在資料瀏覽期間建立的點選連結報表。 
  `LoadReportDefinition` 方法的所有呼叫都會被封鎖。  
  
 關閉此選項可減少惡意使用者利用 `LoadReportDefinition` 要求讓報表伺服器超過負載，藉以啟動阻斷服務攻擊的威脅。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表伺服器屬性 &#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [連接至 Management Studio 中的報表伺服器](connect-to-a-report-server-in-management-studio.md)   
 [指定報表資料來源的認證和連接資訊](..[Management Studio F1 說明中的/Report-data/specify-credential-and-connection-information-for-report-data-sources.md 報表伺服器](report-server-in-management-studio-f1-help.md)  
  
  
