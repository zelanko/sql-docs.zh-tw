---
title: Reporting Services 登入對話方塊 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportservicelogin.f1
ms.assetid: 2037d797-0b61-44c7-931f-6c689c3fc733
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 232ee51614a668b07263c3e3a4182f23652135bf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66099864"
---
# <a name="reporting-services-login-dialog-box-ssrs"></a>Reporting Services 登入對話方塊 (SSRS)
  使用 **[Reporting Services 登入]** 對話方塊，即可提供發行報表至報表伺服器的認證。  
  
-   **注意**如果這是您第一次將報表發行至報表伺服器，因為設定了專案的部署屬性**TargetServerURL** ，請確認您指定的伺服器名稱類似于`http://localhost/reportserver`，而不`http://localhost/reports`是。 如果是指定本機伺服器的 `reports` 目錄，而不是 `reportserver` 目錄，則會間接導致此對話方塊開啟。 如需設定 **TargetServerURL** 的詳細資訊，請參閱[設定部署屬性 &#40;Reporting Services&#41;](set-deployment-properties-reporting-services.md)。  
  
## <a name="options"></a>選項。  
 **Server**  
 顯示報表伺服器的名稱。 例如： `http://localhost/reportserver` 。 如果報表伺服器使用的是預設通訊埠 80 以外的通訊埠，請加入該通訊埠號碼。 例如： `http://localhost:81/reportserver` 。  
  
 **使用者名稱**  
 輸入使用者名稱以登入 Web 服務。  
  
 **密碼**  
 輸入密碼以登入 Web 服務。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 中的資料連線、資料來源及連接字串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [指定報表資料來源的認證和連接資訊](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)[報表設計師 F1](report-designer-f1-help.md)說明  
  
  
