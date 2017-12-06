---
title: "伺服器屬性 (一般頁面) | Microsoft Docs"
ms.custom: 
ms.date: 06/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: tools
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.reportserver.serverproperties.general.f1
ms.assetid: 23537d52-4356-450f-a671-5921cef2431f
caps.latest.revision: "34"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5f1d89a19a2d57ff755b5c3b8c06d11cfce9a569
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="report-server-properties-general-page"></a>報表伺服器屬性 (一般頁面)
  您可以使用這個頁面來檢視或修改在報表管理員中使用的標題、啟用或停用 [我的報表]、針對 [我的報表] 安全性選取角色定義，以及啟用或停用用戶端列印控制項。  
  
 **若要開啟此頁面：**
 1) 啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]
 2) 連接到報表伺服器執行個體。
 3) 以滑鼠右鍵按一下報表伺服器名稱，然後選取 [屬性]。  
  
 伺服器模式會決定您可以設定的伺服器屬性。 如果您要管理針對 SharePoint 整合模式所設定的報表伺服器，便無法啟用 [我的報表] 或設定入口網站的標題。  
  
## <a name="options"></a>選項。  
 **名稱**  
 輸入要顯示在入口網站頂端的名稱。 根據預設，此值為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 所指定的名稱只會出現在報表管理員中。  
  
 **版本(Version)**  
 此屬性是唯讀的。 指定您要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本。  
  
 **版本(Edition)**  
 此屬性是唯讀的。 指定目前的報表伺服器執行個體。 並非所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 **驗證模式**  
 此屬性是唯讀的。 它會識別報表伺服器執行個體所接受之驗證要求的類型。 若要變更驗證模式，您必須編輯 **RSReportServer.config** 檔案。 如需詳細資訊，請參閱 [Authentication with the Report Server](../../reporting-services/security/authentication-with-the-report-server.md)。  
  
 **URL**  
 此屬性是唯讀的。 指定報表伺服器 Web 服務的 URL。 這個值是在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具中指定的。 如需詳細資訊，請參閱[設定 URL &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)。  
  
 **為每個使用者啟用 [我的報表] 資料夾**  
 讓使用者可以使用 [我的報表]。 這個選項僅適用於原生模式報表伺服器。  
  
 **選取要套用至每個 [我的報表] 資料夾的角色**  
 指定要用於 [我的報表] 安全性的角色定義。 角色定義會識別每個 [我的報表] 資料夾中所支援的這組工作。  

  
## <a name="see-also"></a>另請參閱  
 [設定報表伺服器屬性 &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [連接至 Management Studio 中的報表伺服器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [啟用與停用我的報表](../../reporting-services/report-server/enable-and-disable-my-reports.md)   
 [Management Studio F1 說明中的報表伺服器](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [保護我的報表](../../reporting-services/security/secure-my-reports.md)  
  
  

