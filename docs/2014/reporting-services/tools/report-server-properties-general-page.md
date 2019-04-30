---
title: 伺服器屬性 (一般頁面) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.general.f1
ms.assetid: 23537d52-4356-450f-a671-5921cef2431f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 578d824aa4438ce45dda223c040aa06e8bc9c6f7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63201379"
---
# <a name="server-properties-general-page"></a>伺服器屬性 (一般頁面)
  您可以使用這個頁面來檢視或修改在報表管理員中使用的標題、啟用或停用 [我的報表]、針對 [我的報表] 安全性選取角色定義，以及啟用或停用用戶端列印控制項。  
  
 若要開啟此頁面，請啟動[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，連接到報表伺服器執行個體，以滑鼠右鍵按一下報表伺服器名稱，然後選取**屬性**。  
  
 伺服器模式會決定您可以設定的伺服器屬性。 如果您要管理針對 SharePoint 整合模式所設定的報表伺服器，便無法啟用 [我的報表] 或設定報表管理員的應用程式標題。  
  
## <a name="options"></a>選項。  
 **名稱**  
 鍵入報表管理員中顯示的應用程式名稱。 根據預設，此值為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 所指定的名稱只會出現在報表管理員中。  
  
 **版本(Version)**  
 此屬性是唯讀的。 指定您要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本。  
  
 **版本(Edition)**  
 此屬性是唯讀的。 指定目前的報表伺服器執行個體。 並非所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需的版本所支援的功能清單[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱 <<c2> [ 支援的 SQL Server 2014 的版本功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
 **驗證模式**  
 此屬性是唯讀的。 它會識別報表伺服器執行個體所接受之驗證要求的類型。 若要變更驗證模式，您必須編輯 RSReportServer.config 檔。 如需詳細資訊，請參閱 [Authentication with the Report Server](../security/authentication-with-the-report-server.md)。  
  
 **URL**  
 此屬性是唯讀的。 指定報表伺服器 Web 服務的 URL。 這個值是在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態工具中指定的。 如需詳細資訊，請參閱[設定 URL &#40;SSRS 組態管理員&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md)。  
  
 **為每個使用者啟用 [我的報表] 資料夾**  
 讓使用者可以使用 [我的報表]。 這個選項僅適用於原生模式報表伺服器。  
  
 **選取要套用至每個 [我的報表] 資料夾的角色**  
 指定要用於 [我的報表] 安全性的角色定義。 角色定義會識別每個 [我的報表] 資料夾中所支援的這組工作。  
  
 **啟用 ActiveX 用戶端列印控制項下載**  
 設定 `EnableClientPrinting` 報表伺服器系統屬性。 如果您啟用了用戶端列印，則擁有本機管理員權限的使用者會有選項可下載已簽署的 ActiveX 控制項以便列印 HTML 報表。 如需詳細資訊，請參閱 [啟用和停用 Reporting Services 的用戶端列印](../report-server/enable-and-disable-client-side-printing-for-reporting-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表伺服器屬性 &#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [連接至 Management Studio 中的報表伺服器](connect-to-a-report-server-in-management-studio.md)   
 [啟用與停用我的報表](../report-server/enable-and-disable-my-reports.md)   
 [Management Studio F1 說明中的報表伺服器](report-server-in-management-studio-f1-help.md)   
 [保護我的報表](../security/secure-my-reports.md)  
  
  
