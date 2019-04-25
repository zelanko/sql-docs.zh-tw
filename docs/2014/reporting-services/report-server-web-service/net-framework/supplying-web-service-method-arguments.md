---
title: 提供 Web 服務方法引數 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Report Server Web service, methods
- Web service [Reporting Services], methods
- methods [Reporting Services], arguments
- XML Web service [Reporting Services], methods
ms.assetid: f7b9ca05-fc4c-4b30-8e5d-172dd0f4a832
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3ef5188934628589751fe92d1839da0efb265766
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62522222"
---
# <a name="supplying-web-service-method-arguments"></a>提供 Web 服務方法引數
  報表伺服器 Web 服務方法會透過 HTTP 使用 SOAP 在指定的 URL 傳送要求給服務。 服務會接收要求、處理要求，然後傳回回應。 這些要求和回應是 XML 文件的形式。  
  
## <a name="optional-parameters"></a>選擇性參數  
 在某些情況下，Web 服務方法可以有選擇性的輸入參數。 即使 Web 服務方法的輸入參數是選擇性的，仍然必須包括它，並將參數值設定為 `null` ([!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 中的 `Nothing`)。 將參數值設定為 `null`，會將 SOAP 要求中該參數的元素值設定為 `null`。  
  
 下列範例會使用 <xref:ReportService2010.ReportingService2010.CreateFolder%2A> 方法在 Sales 資料夾中建立名為 Product Sales 的新資料夾。 透過為資料夾屬性提供 `null` 值，就不會為資料夾提供使用者特定屬性：  
  
```  
// C#  
rs.CreateFolder("Product Sales", "/Sales", null);  
```  
  
## <a name="complex-data-types"></a>複雜的資料類型  
 報表伺服器 Web 服務的核心類別是 <xref:ReportService2010.ReportingService2010>，您使用它來叫用 SOAP 作業或是 Proxy 類別的 Web 方法。 若要支援此類別及其方法，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 包括使用者定義、複雜的資料類型，這些資料類型是 Web 服務方法的輸入與輸出參數特有的。 這些複雜的資料類型是產生之 Proxy 類別的一部分，可在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 環境中開發時使用。  
  
 當您產生 Proxy 類別時，在 WSDL 檔案中定義的複雜資料類型是由 Proxy 類別所代表，這包括對應至複雜資料類型的各種 SOAP 元素。 這些資料類型的順序會變成可在程式碼中列舉的物件陣列。 這會列舉直接與 SOAP 訊息中傳送的 XML 結構搭配使用的需求。 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 會為您處理翻譯。  
  
## <a name="see-also"></a>另請參閱  
 [使用 Web 服務和 .NET Framework 建置應用程式](building-applications-using-the-web-service-and-the-net-framework.md)   
 [報表伺服器 Web 服務](../report-server-web-service.md)   
 [技術參考 &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  
