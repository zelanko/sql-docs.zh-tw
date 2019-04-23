---
title: Reporting Services 安全性與保護 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- security [Reporting Services]
- Reporting Services, security
ms.assetid: 270075c5-bf12-4467-a775-abbda3d954a5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ca88c252e37362f2a5b64bb8d41ebac27f0e24dd
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59943134"
---
# <a name="reporting-services-security-and-protection"></a>Reporting Services 安全性與保護
  您可以使用本節的資訊，了解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 本節也將說明 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中所支援的授權模型和驗證提供者。  
  
## <a name="extended-protection-for-authentication"></a>驗證擴充保護  
 從 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]開始，就有驗證擴充保護的支援可以使用。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能可支援使用通道繫結和服務繫結，以增強驗證的保護。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能需要搭配支援擴充保護的作業系統使用。 如需詳細資訊，請參閱 [Extended Protection for Authentication with Reporting Services](extended-protection-for-authentication-with-reporting-services.md)。  
  
## <a name="authentication-and-authorization"></a>驗證與授權  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會提供不同的使用者驗證類型和用戶端應用程式，便於使用報表伺服器進行驗證。 為您的報表伺服器使用正確的驗證類型可讓組織獲得組織所需之適當的安全性層級。 如需詳細資訊，請參閱 [Authentication with the Report Server](authentication-with-the-report-server.md)。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 也會採用角色和權限，控制使用者在報表伺服器目錄中的內容存取 (換句話說，可存取的人員以及存取的方式)。 如需詳細資訊，請參閱[角色與權限 &#40;Reporting Services&#41;](roles-and-permissions-reporting-services.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|連結|  
|-----------------------|-----------|  
|設定 Secure Socket Layer (SSL) 可保護連線至報表伺服器的用戶端。|[在原生模式報表伺服器上設定 SSL 連接](configure-ssl-connections-on-a-native-mode-report-server.md)|  
  
  
