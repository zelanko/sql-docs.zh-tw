---
title: "Reporting Services SoapException 類別 |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
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
- exceptions [Reporting Services], SoapException class
- SoapException class
ms.assetid: 2cec49ee-20b1-40eb-a75b-0908d9c05b34
caps.latest.revision: 33
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: e24a518bee7b192505fc93ad26d4345f9d710143
ms.contentlocale: zh-tw
ms.lasthandoff: 08/12/2017

---
# <a name="reporting-services-soapexception-class"></a>Reporting Services SoapException 類別
  您應該處理可能會發生的特定 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 錯誤。 例如，在您詢問使用者是否建立資料夾的應用程式中，使用者或許會嘗試建立已經存在的資料夾。 身為開發人員，您無法控制使用者在應用程式的資料夾名稱與路徑欄位中輸入的內容，但是，您卻可以控制使用者在試圖建立已經存在的項目時所得到的體驗。  
  
 若要讓您更輕鬆地找出特定錯誤狀況，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]分類例外狀況的錯誤代碼，並傳回錯誤時使用屬性的分類**SoapException**類別。 如需詳細資訊，請參閱 < SoapException 類別 > [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK 文件。  
  
 下表列出的公用屬性**SoapException**類別。  
  
|公用屬性|Description|  
|---------------------|-----------------|  
|**動作項目**|造成例外狀況的程式碼， 這個值是 Web 服務方法的 URL。|  
|**詳細資料**|應用程式特定的錯誤資訊， 這個值是由報表伺服器所設定，且格式為 XML。 如需詳細資訊，請參閱[Detail 屬性](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)和[使用處理特定錯誤的詳細資料屬性](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)。|  
|**HelpLink**|與該錯誤相關聯的說明檔之 URL 或 URN。 這個值通常是由 Web 服務所設定，而且它會將 URL 設定為 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 說明與支援。 因為[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]支援多個說明連結是否錯誤發生時，報表伺服器設定說明連結資訊的一部分**詳細**屬性。 如需詳細資訊，請參閱[HelpLink 元素](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/helplink-element.md)。|  
|**訊息**|描述錯誤的當地語系化描述性訊息。 此文字可能會出現在應用程式 UI 中。|  
  
## <a name="see-also"></a>另請參閱  
 [例外狀況處理中的 Reporting Services 簡介](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [SoapException 錯誤資料表](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md)  
  
  
