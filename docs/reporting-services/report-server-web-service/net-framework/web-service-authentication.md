---
title: Web 服務驗證 | Microsoft Docs
description: 如果用戶端對報表伺服器發出 SOAP 要求，請實作驗證的用戶端部分。 了解如何實作 Web 服務的驗證。
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], authentication
- XML Web service [Reporting Services], authentication
- Report Server Web service, authentication
ms.assetid: 852b4947-a090-4e54-8555-5a503945ceab
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 34873835231c122f3d086c3490be2bab7a684925
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "79198530"
---
# <a name="web-service-authentication"></a>Web 服務驗證
  您可以使用 Windows 驗證或是基本驗證，以驗證對報表伺服器 Web 服務的呼叫。 任何對報表伺服器提出 SOAP 要求的用戶端，都必須實作其中一個支援的驗證通訊協定之用戶端部分。 如果您正在使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]，則可使用受控碼 HTTP 類別來實作驗證。 使用這些 API 使得連同 SOAP 要求一起傳送驗證資訊變得更容易。  
  
 如果在呼叫報表伺服器 Web 服務之前沒有適當的認證，呼叫會失敗。 在執行階段時，您可以藉由在呼叫其方法之前，設定表示 Web 服務之用戶端物件的 **Credentials** 屬性，將認證傳遞至 Web 服務。  
  
 下列小節包含使用 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 傳送認證的範例程式碼。  
  
## <a name="windows-authentication"></a>Windows 驗證  
 下列程式碼將 Windows 認證傳遞到 Web 服務。  
  
```vb  
Dim rs As New ReportingService()  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
```  
  
```csharp  
ReportingService rs = new ReportingService();  
rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
```  
  
## <a name="basic-authentication"></a>基本驗證  
 下列程式碼將基本認證傳遞到 Web 服務。  
  
```vb  
Dim rs As New ReportingService()  
rs.Credentials = New System.Net.NetworkCredential("username", "password", "domain")  
```  
  
```csharp  
ReportingService service = new ReportingService();  
service.Credentials = new System.Net.NetworkCredential("username", "password", "domain");  
```  
  
 在您呼叫報表伺服器 Web 服務的任何方法之前，必須先設定認證。 如果您未設定認證，會收到錯誤碼「HTTP 401 錯誤：拒絕存取」。 您必須在使用它之前先驗證服務，但是在您設定認證之後，不需要再次設定它們，因為您會繼續使用相同的服務變數 (例如，*rs*)。  
  
## <a name="custom-authentication"></a>自訂驗證  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 包括程式設計 API，以提供開發人員設計和開發自訂驗證延伸模組的機會，又稱為安全性延伸模組。 如需詳細資訊，請參閱＜ [Implementing a Security Extension](../../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [使用 Web 服務和 .NET Framework 建置應用程式](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [報表伺服器 Web 服務](../../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
