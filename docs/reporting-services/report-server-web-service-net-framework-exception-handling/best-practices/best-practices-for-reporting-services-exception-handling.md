---
title: "Reporting Services 例外處理的最佳作法 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
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
- exceptions [Reporting Services], best practices
ms.assetid: 72fecf28-f02e-4338-b50f-0b21f520302d
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 8f6546605af6bb6c23b6b380fbaf7042d093addf
ms.contentlocale: zh-tw
ms.lasthandoff: 08/12/2017

---
# <a name="best-practices-for-reporting-services-exception-handling"></a>Reporting Services 例外處理的最佳作法
  當開發 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 應用程式時，您可以使用幾個方法來消除或是減少例外狀況的發生次數。 當例外狀況真的發生時，提供明確且精簡的錯誤訊息給使用者，並加入適當的例外狀況處理，以防止應用程式非預期地結束。  
  
 將要求傳送給報表伺服器 Web 服務的應用程式應該執行下列項目：  
  
-   透過盡可能防止無效的要求以避免造成例外狀況。  
  
-   盡可能快取例外狀況並提供特定的錯誤處理程式碼。  
  
-   處理未擲回例外狀況的錯誤案例。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[防止無效的要求](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/preventing-invalid-requests.md)|描述可用以防止將無效的要求傳送到報表伺服器的技術。|  
|[使用 Try 和 Catch 區塊](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-try-and-catch-blocks.md)|描述如何進一步使用 Try/Catch 區塊來增強應用程式的可靠性。|  
|[處理未造成例外狀況的警告與案例](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/handling-warnings-and-cases-that-do-not-cause-exceptions.md)|說明如何處理錯誤才不會造成 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 擲回例外狀況。|  
|[使用詳細資料屬性來處理特定的錯誤](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)|說明如何以程式設計方式處理使用的特定錯誤**詳細**屬性**SoapException**物件。|  
  
## <a name="see-also"></a>另請參閱  
 [Detail 屬性](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)   
 [例外狀況處理中的 Reporting Services 簡介](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 類別](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
