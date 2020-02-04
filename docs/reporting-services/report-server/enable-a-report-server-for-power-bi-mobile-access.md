---
title: 啟用報表伺服器進行 Power BI 行動存取 | Microsoft Docs
ms.date: 12/17/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: c1a71522-394b-46a7-b9ec-f964bdd81d82
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d14c8e092a030c88dbc4d0b5d4375bb56a8eb82c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "63308175"
---
# <a name="enable-a-report-server-for-power-bi-mobile-access"></a>啟用報表伺服器進行 Power BI 行動存取
您可以使用 Power BI 行動應用程式使用行動報表。 您必須設定幾個項目，允許 Power BI 行動應用程式連接到 Reporting Services。  
  
-   [行動報表需要 Reporting Services 原生模式](#nativemode)  
-   [啟用 Reporting Services 的基本驗證](#basicauth) (適用於 CTP 3.2)  
-   [用戶端裝置建議啟用 HTTPS 和有效的憑證信任](#https)  
-   [檢閱防火牆設定](#firewall)  
  
<a name="nativemode"/>  
## <a name="reporting-services-native-mode-required"></a>需要 Reporting Services 原生模式  
行動報表是原生模式的功能。 SharePoint 整合模式不提供。 Power BI 行動應用程式只適用於原生模式執行個體。  
  
<a name="basicauth"/>  
## <a name="enable-basic-authentication"></a>啟用基本驗證  
iOS Power BI 行動應用程式需要基本驗證，才能連接並使用行動報表。 Reporting Services 設定預設不啟用基本驗證。 如需如何設定基本驗證的資訊，請參閱 [設定報表伺服器的基本驗證](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)。  
  
您也必須啟用 Windows 驗證，允許發行者應用程式發行行動報表。  
  
<a name="https"/>  
## <a name="enable-https"></a>啟用 HTTPS  
如果啟用基本驗證，建議您在 Reporting Services 中啟用 HTTPS。 如果啟用了 HTTPS，請確定所用憑證是執行 iOS Power BI 行動應用程式的用戶端裝置可以信任的憑證。 這表示憑證鏈結必須是有效且可用於用戶端裝置。  
  
如果開發或評估需要使用自我簽署的憑證，您可以從報表伺服器匯出憑證，並將它安裝在行動裝置上。 請參閱裝置文件，了解如何將它安裝在裝置上。  
  
如需啟用 SSL 的詳細資訊，請參閱 [在原生模式報表伺服器上設定 SSL 連接](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)。  
  
<a name="firewall"/>  
## <a name="review-firewall-settings"></a>檢閱防火牆設定  
建議您檢閱防火牆設定，以確保所有裝置都能成功連接到 Reporting Services。   
  
如需如何設定 Windows 防火牆的詳細資訊，請參閱 [設定報表伺服器存取的防火牆](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)。  
  
## <a name="see-also"></a>另請參閱  
  
[設定報表伺服器上的基本驗證](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)  
[在原生模式報表伺服器上設定 SSL 連線](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)  
[設定供報表伺服器存取的防火牆](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
  
  
  
  
  
  

