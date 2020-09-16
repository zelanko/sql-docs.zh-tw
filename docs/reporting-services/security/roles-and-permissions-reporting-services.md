---
description: 角色與權限 (Reporting Services)
title: 角色與權限 (Reporting Services) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- access controls [Reporting Services]
- permissions [Reporting Services], about permissions
- security [Reporting Services], identity and access control
- authentication [Reporting Services]
- permissions [Reporting Services]
- security [Reporting Services], role-based
- identity [Reporting Services]
ms.assetid: eea655fe-43ed-418d-8233-b288a8f4daa4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 18dbb9344ff8dd2284ba200dc667057ffbeedf44
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498021"
---
# <a name="roles-and-permissions-reporting-services"></a>角色與權限 (Reporting Services)
  Reporting Services 會提供驗證子系統和以角色為基礎的授權模型。 驗證和授權模型會因報表伺服器是以原生模式或 SharePoint 模式執行而不同。 如果報表伺服器屬於 SharePoint 部署的一部分，SharePoint 權限將決定擁有報表伺服器存取權的人員。  
  
## <a name="identity-and-access-control-for-native-mode"></a>原生模式的識別和存取控制  
 預設驗證是以 Windows 驗證和整合式安全性為基礎。 您可變更這些驗證設定，以便允許報表伺服器回應不同的驗證要求，甚至是將預設的安全性功能取代成您提供的自訂驗證延伸模組。  
  
 授權是以您指派給原則的角色為基礎。 每個角色都包含一組相關的工作，然後這些工作則包含相關的作業。 例如，[管理報表]**** 工作會授與下列報表伺服器作業的存取權：檢視報表、新增報表、更新報表、刪除報表、排程報表和更新報表屬性。  
  
## <a name="identity-and-access-control-for-sharepoint-mode"></a>SharePoint 模式的識別和存取控制  
 在 SharePoint 整合模式中，驗證和授權會先在 SharePoint 網站上處理，然後要求才會送達報表伺服器。 根據您設定驗證的方式而定，來自 SharePoint 網站的要求會包含安全性 Token 或受信任的使用者名稱。 您針對 SharePoint 使用者和群組所設定的權限會授權放置於 SharePoint 文件庫中之報表伺服器項目的存取權。  
  
## <a name="in-this-section"></a>本節內容  
 [在原生模式報表伺服器上授與權限](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
 描述提供內容和作業之存取權的以角色為基礎授權模型。  
  
 [授與 SharePoint 網站上報表伺服器項目的權限](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
 說明 SharePoint 群組、權限等級和權限如何用於控制報表伺服器的存取權。  
  
## <a name="see-also"></a>另請參閱  
 [使用報表伺服器驗證](../../reporting-services/security/authentication-with-the-report-server.md)   
 [在原生模式報表伺服器上授與權限](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
