---
title: "提供 Web 服務方法引數 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Report Server Web service, methods
- Web service [Reporting Services], methods
- methods [Reporting Services], arguments
- XML Web service [Reporting Services], methods
ms.assetid: f7b9ca05-fc4c-4b30-8e5d-172dd0f4a832
caps.latest.revision: 38
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 761571f88c2321c823dc240cfa9bb3ba75d9414b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="supplying-web-service-method-arguments"></a>提供 Web 服務方法引數
  報表伺服器 Web 服務方法會透過 HTTP 使用 SOAP 在指定的 URL 傳送要求給服務。 服務會接收要求、處理要求，然後傳回回應。 這些要求和回應是 XML 文件的形式。  
  
## <a name="optional-parameters"></a>選擇性參數  
 在某些情況下，Web 服務方法可以有選擇性的輸入參數。 即使 Web 服務方法的輸入的參數是選擇性的您仍然必須將它包含並將參數值設定為**null** (**Nothing**中[!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)])。 將參數值設定為**null**的元素值設定為該參數的 SOAP 要求中**null**。  
  
 下列範例會使用 <xref:ReportService2010.ReportingService2010.CreateFolder%2A> 方法在 Sales 資料夾中建立名為 Product Sales 的新資料夾。 藉由提供**null**資料夾會提供資料夾內容中沒有使用者特定屬性的值：  
  
```  
// C#  
rs.CreateFolder("Product Sales", "/Sales", null);  
```  
  
## <a name="complex-data-types"></a>複雜的資料類型  
 報表伺服器 Web 服務的核心類別是 <xref:ReportService2010.ReportingService2010>，您使用它來叫用 SOAP 作業或是 Proxy 類別的 Web 方法。 若要支援此類別及其方法，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 包括使用者定義、複雜的資料類型，這些資料類型是 Web 服務方法的輸入與輸出參數特有的。 這些複雜的資料類型是產生的 proxy 類別，您可以用在開發時的一部分[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]環境。  
  
 當您產生 Proxy 類別時，在 WSDL 檔案中定義的複雜資料類型是由 Proxy 類別所代表，這包括對應至複雜資料類型的各種 SOAP 元素。 這些資料類型的順序會變成可在程式碼中列舉的物件陣列。 這會列舉直接與 SOAP 訊息中傳送的 XML 結構搭配使用的需求。 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 會為您處理翻譯。  
  
## <a name="see-also"></a>另請參閱  
 [使用 Web 服務和.NET Framework 建置應用程式](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [報表伺服器 Web 服務](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [技術參考 &#40;SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
