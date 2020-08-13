---
title: 伺服器屬性 (記錄頁面) | Microsoft Docs
description: 了解如何使用 SQL Server Management Studio 中 [Reporting Services] 頁面上的選項，以設定報表伺服器所收集報表執行資料的限制。
ms.date: 06/10/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.serverproperties.logging.f1
ms.assetid: b338deab-4868-4951-9f22-0605add2fc95
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8b06ebb1151d68b462fa96cd1c7493460209d33d
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912394"
---
# <a name="server-properties-logging-page"></a>伺服器屬性 (記錄頁面)
  使用 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 中的這個 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 頁面，即可對報表伺服器所收集的報表執行資料設定限制。 執行資料會儲存在報表伺服器資料庫內部。 您可以針對以原生模式或 SharePoint 整合模式執行的報表伺服器追蹤報表活動。 如果報表伺服器屬於向外延展部署的一部分，報表執行記錄就會在單一記錄檔中維護整個部署之所有報表活動的記錄。  
  
 開啟此頁面：
 1) 啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]
 2) 連接到報表伺服器。
 3) 以滑鼠右鍵按一下報表伺服器名稱，然後選取 [屬性]。 
 4) 按一下 **[記錄]** ，即可開啟此頁面。  
  
## <a name="options"></a>選項。  
 **啟用報表執行記錄**  
 按一下即可建立和儲存有關伺服器之報表活動的資訊。 如果此選項已啟用，報表伺服器將會追蹤使用的報表、報表處理的頻率、執行的報表作業類型、輸出格式，以及執行報表的人員。 如需記錄中擷取之其他資料點的詳細資訊，請參閱 [報表伺服器 ExecutionLog 和 ExecutionLog3 檢視](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)。  
  
 **移除此天數之前的記錄項目**  
 指定天數，在此天數後的記錄項目會從報表執行記錄中刪除。 預設值為 60 天。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表伺服器屬性 &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [連接至 Management Studio 中的報表伺服器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Reporting Services 記錄檔和來源](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [Management Studio F1 說明中的報表伺服器](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [報表伺服器 ExecutionLog 和 ExecutionLog3 檢視](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)  
  
  
