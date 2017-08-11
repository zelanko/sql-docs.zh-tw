---
title: "Reporting Services 登入對話方塊 (SSRS) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- sql13.rtp.rptdesigner.reportservicelogin.f1
ms.assetid: 2037d797-0b61-44c7-931f-6c689c3fc733
caps.latest.revision: 31
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3f9da76454e0b1fe52499471cbb3a04ada2d896e
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="reporting-services-login-dialog-box-ssrs"></a>Reporting Services 登入對話方塊 (SSRS)
  使用 **[Reporting Services 登入]** 對話方塊，即可提供發行報表至報表伺服器的認證。  
  
-   **注意** ：如果這是您在設定專案的 **TargetServerURL** 部署屬性之後第一次將報表發行到報表伺服器，請確認所指定的伺服器名稱包含 **server** ，而不是 **reports**。 例如， `http://localhost/reportserver`，而不是 `http://localhost/reports`。 如果是指定本機伺服器的 `reports` 目錄，而不是 `reportserver` 目錄，則會間接導致此對話方塊開啟。 如需設定 **TargetServerURL** 的詳細資訊，請參閱[設定部署屬性 &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)。  
  
## <a name="options"></a>選項。  
 **Server**  
 顯示報表伺服器的名稱。 例如， `http://localhost/reportserver`。 如果報表伺服器使用的是預設通訊埠 80 以外的通訊埠，請加入該通訊埠號碼。 例如， `http://localhost:81/reportserver`。  
  
 **使用者名稱**  
 輸入使用者名稱以登入 Web 服務。  
  
 **密碼**  
 輸入密碼以登入 Web 服務。  
  
## <a name="see-also"></a>請參閱＜  
 [資料連接、資料來源及連接字串 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [指定認證和報表資料來源的連接資訊](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [報表設計師 F1 說明](../../reporting-services/tools/report-designer-f1-help.md)  
  
  
