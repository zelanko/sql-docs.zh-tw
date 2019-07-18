---
title: Reporting Services 中的 SOAP 角色 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], SOAP
- SOAP [Reporting Services], role in Reporting Services
- Report Server Web service, SOAP
- XML Web service [Reporting Services], SOAP
ms.assetid: f229c3ef-f2ca-448f-98f1-b8df350b9992
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4e0b418e44436912b5ed1368ad7a316951872266
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62519196"
---
# <a name="the-role-of-soap-in-reporting-services"></a>The Role of SOAP in Reporting Services
  報表伺服器 Web 服務透過網路使用簡易物件存取通訊協定 (SOAP) 訊息，傳送以文字為基礎的命令。 這些命令使用 XML 文字的格式，以 HTTP 透過全球資訊網來傳送文字。 透過使用 SOAP 做為其通訊協定，報表伺服器 Web 服務允許應用程式和元件使用開放且廣為接受的基礎結構，來與報表伺服器交換資料。 SOAP 標準是定義在 www.w3.org/TR/SOAP。  
  
 任何用戶端應用程式都可以當做 SOAP 用戶端使用，只要它是 SOAP 感知並且可傳送 SOAP 要求。 報表管理員就是這類的 SOAP 用戶端。 它提供儲存所有報表與報表相關內容之報表伺服器資料庫的介面。 使用者可以使用應用程式，來瀏覽和管理報表伺服器命名空間中的報表與資料夾。 報表管理員是建立在報表伺服器 Web 服務基礎結構上。  
  
 報表伺服器可做為 SOAP 伺服器，這是可從 SOAP 用戶端接受要求並建立適當回應的 SOAP 感知服務。 伺服器會處理要求並將編碼的回應傳回用戶端。  
  
 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的 SOAP 訊息有許多不同的形式，端視用戶端所提出的要求類型而定。 下列範例代表簡單的 SOAP 用戶端要求，以移除報表伺服器資料庫中的項目。  
  
```  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
    <soap:Body>  
        <DeleteItem xmlns="https://www.microsoft.com/sql/ReportingServer">  
            <item>/Samples/Report1</item>  
        </DeleteItem>  
    </soap:Body>  
</soap:Envelope>  
```  
  
 SOAP 本身需要將訊息放入 `Envelope` 元素中，並且在 `Body` 元素中含有大量的訊息。 在此範例中，本文包含對 <xref:ReportService2010.ReportingService2010.DeleteItem%2A> 方法的呼叫，這需要代表要刪除的項目路徑之字串參數。 您可以建立 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 用戶端 Proxy 類別，將所有的 SOAP 作業封裝成方法。 下列 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] 方法代表稍早指定的 SOAP 範例。  
  
```  
public void DeleteItem(string item);  
```  
  
 伺服器的回應可能如下所示：  
  
```  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
    <soap:Body>  
        <DeleteItemResponse xmlns="https://www.microsoft.com/sql/ReportingServer" />  
    </soap:Body>  
</soap:Envelope>  
```  
  
 <xref:ReportService2010.ReportingService2010.DeleteItem%2A> 方法沒有傳回值，所以會傳回空的回應。  
  
## <a name="see-also"></a>另請參閱  
 [存取 SOAP API](accessing-the-soap-api.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)   
 [Reporting Services Report Server](../reporting-services-report-server.md)   
 [報表伺服器 Web 服務](report-server-web-service.md)  
  
  
