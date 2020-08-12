---
title: 安全性延伸模組概觀 | Microsoft Docs
description: 了解 Reporting Services 中的安全性延伸模組。 了解適合使用自訂驗證和授權的情況。
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- security [Reporting Services], extensions
ms.assetid: 24ccd795-6506-457c-93ac-6a9dd6bb9a46
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 72eaf9b5c47d19da6b7f1893e473031cd6ebc615
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529194"
---
# <a name="security-extensions-overview---reporting-services-ssrs"></a>安全性延伸模組 - Reporting Services (SSRS)
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 安全性延伸模組會啟用使用者或群組的驗證和授權；也就是說，它會讓不同的使用者登入到報表伺服器，並根據其識別執行不同的工作或作業。 依預設，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 會使用 Windows 架構的驗證延伸模組，此模組使用 Windows 帳戶通訊協定來確認宣稱在系統上具有帳戶之使用者的識別。 以 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 會使用以角色為基礎的安全性系統來授權使用者。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 以角色為基礎的安全性模型類似於其他技術以角色為基礎的安全性模型。  
  
 因為安全性延伸模組是以開放且可延伸的 API 為基礎，所以您可以在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中建立新的驗證和授權延伸模組。 以下是一般安全性延伸模組實作的範例，此實作會使用以表單為基礎的驗證和授權：  
  
 ![Reporting Services 安全性延伸模組處理序](../../../reporting-services/extensions/security-extension/media/rosettasecurityextensionflow.gif "Reporting Services 安全性延伸模組處理序")  
  
 如下圖所顯示，驗證和授權的進行方式如下：  
  
1.  使用者使用 URL 來嘗試存取入口網站，然後被重新導向至針對用戶端應用程式收集使用者認證的表單。  
  
2.  使用者將認證提交給表單。  
  
3.  使用者認證透過 <xref:ReportService2010.ReportingService2010.LogonUser%2A> 方法提交給 Reporting Services Web 服務。  
  
4.  Web 服務呼叫客戶所提供的安全性延伸模組，並且確認自訂的安全性授權中具有使用者名稱和密碼。  
  
5.  在進行驗證後，Web 服務會建立驗證票證 (也稱為 "Cookie")、管理票證，然後針對入口網站的首頁確認使用者的角色。  
  
6.  Web 服務將 Cookie 傳回給瀏覽器，並在入口網站中顯示適當的使用者介面。  
  
7.  在使用者經過驗證後，瀏覽器會以 HTTP 標頭傳送 Cookie 以對入口網站提出要求。 這些要求是用於回應入口網站中的使用者動作。  
  
8.  Cookie 會在 HTTP 標頭中，與所要求的使用者作業一起傳送給 Web 服務。  
  
9. 對 Cookie 進行驗證，如為有效，則報表伺服器會從報表伺服器資料庫傳回安全性描述項，以及與所要求作業相關的其他資訊。  
  
10. 如果 Cookie 有效，則報表伺服器會呼叫安全性延伸模組，以檢查是否授權使用者執行特定的作業。  
  
11. 如果使用者已獲得授權，則報表伺服器會執行要求的作業，並將控制項傳回給呼叫者。  
  
12. 在使用者經過驗證後，對報表伺服器的 URL 存取會使用相同的 Cookie。 Cookie 會以 HTTP 標頭傳輸。  
  
13. 使用者會繼續在報表伺服器上要求作業，直到工作階段結束。  
  
## <a name="when-to-implement-a-security-extension"></a>何時實作安全性延伸模組  
 我們建議您盡可能使用 Windows 驗證。 不過，下列兩個案例可能比較適合 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的自訂驗證和授權：  
  
-   您具有無法使用 Windows 帳戶的網際網路或外部網路應用程式。  
  
-   您具有自訂的使用者和角色，而且需要在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中提供相符的授權配置。  
  
## <a name="see-also"></a>另請參閱  
 [實作安全性延伸模組](../../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)   
  
  
