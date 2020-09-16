---
description: Reporting Services 安全性與保護
title: Reporting Services 安全性與保護 | Microsoft Docs
ms.date: 08/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- security [Reporting Services]
- Reporting Services, security
ms.assetid: 270075c5-bf12-4467-a775-abbda3d954a5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e81ddb5a5255f8f7f03491709ae77da47a398de9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480700"
---
# <a name="reporting-services-security-and-protection"></a>Reporting Services 安全性與保護
  您可以使用本節的資訊，了解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 本節也將說明 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中所支援的授權模型和驗證提供者。  
  
## <a name="extended-protection-for-authentication"></a>驗證擴充保護  
 從 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]開始，就有驗證擴充保護的支援可以使用。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能可支援使用通道繫結和服務繫結，以增強驗證的保護。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能需要搭配支援擴充保護的作業系統使用。 如需詳細資訊，請參閱 [Extended Protection for Authentication with Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)。  
  
## <a name="authentication-and-authorization"></a>驗證和授權  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會提供不同的使用者驗證類型和用戶端應用程式，便於使用報表伺服器進行驗證。 為您的報表伺服器使用正確的驗證類型可讓組織獲得組織所需之適當的安全性層級。 如需詳細資訊，請參閱 [Authentication with the Report Server](../../reporting-services/security/authentication-with-the-report-server.md)。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 也會採用角色和權限，控制使用者在報表伺服器目錄中的內容存取 (換句話說，可存取的人員以及存取的方式)。 如需詳細資訊，請參閱[角色與權限 &#40;Reporting Services&#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|連結|  
|-----------------------|-----------|  
|設定傳輸層安全性 (TLS) (先前稱為安全通訊端層 (SSL)) 以保護針對報表伺服器的用戶端連線。|[在原生模式報表伺服器上設定 TLS 連線](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)|  
  
  
