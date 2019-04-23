---
title: Reporting Services 登入對話方塊 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportservicelogin.f1
ms.assetid: 2037d797-0b61-44c7-931f-6c689c3fc733
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7f4753ba89da99753463a852ae38456e56cec3b3
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59960744"
---
# <a name="reporting-services-login-dialog-box-ssrs"></a>Reporting Services 登入對話方塊 (SSRS)
  使用 **[Reporting Services 登入]** 對話方塊，即可提供發行報表至報表伺服器的認證。  
  
-   **附註**如果這是您將報表發行至報表伺服器之後的第一次您設定部署屬性**TargetServerURL**專案，請確認您所指定的伺服器名稱是類似於`http://localhost/reportserver`，而非`http://localhost/reports`。 如果是指定本機伺服器的 `reports` 目錄，而不是 `reportserver` 目錄，則會間接導致此對話方塊開啟。 如需設定 **TargetServerURL** 的詳細資訊，請參閱[設定部署屬性 &#40;Reporting Services&#41;](set-deployment-properties-reporting-services.md)。  
  
## <a name="options"></a>選項。  
 **Server**  
 顯示報表伺服器的名稱。 例如， `http://localhost/reportserver`。 如果報表伺服器使用的是預設通訊埠 80 以外的通訊埠，請加入該通訊埠號碼。 例如， `http://localhost:81/reportserver` 。  
  
 **使用者名稱**  
 輸入使用者名稱以登入 Web 服務。  
  
 **密碼**  
 輸入密碼以登入 Web 服務。  
  
## <a name="see-also"></a>另請參閱  
 [資料連接、 資料來源和 Reporting Services 中的連接字串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [指定認證和報表資料來源的連接資訊](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)[報表設計師 F1 說明](report-designer-f1-help.md)  
  
  
