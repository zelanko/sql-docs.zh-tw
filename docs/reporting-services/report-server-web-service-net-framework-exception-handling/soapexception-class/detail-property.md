---
title: "詳細資料屬性 |Microsoft 文件"
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
- Detail property
- SoapException class
ms.assetid: c1ddaeb6-c540-49fa-b06e-b6359d377ee8
caps.latest.revision: 33
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: f2359ac68758ba2846c4a9065f6cb1c9c96a7e01
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="detail-property"></a>詳細資料屬性
  **詳細**屬性[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] **SoapException**類別具有下列 XML 結構：  
  
## <a name="elements"></a>元素  
 **詳細資料**  
 包含所有其他錯誤詳細資料元素的上層元素。  
  
 **ErrorCode**  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 特定的錯誤碼。  
  
 **HttpStatus**  
 HTTP 狀態碼。  
  
 **訊息**  
 報表伺服器指派的錯誤訊息與錯誤碼。  
  
 **HelpLink**  
 網站的說明連結 URL，在此可以找到有關錯誤的進一步資訊。 如需詳細資訊，請參閱[HelpLink 元素](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/helplink-element.md)。  
  
 **LinkID**  
 指派給該連結的識別碼。  
  
 **產品名稱**  
 產品的名稱。 預設值是**Microsoft SQL Server Reporting Services**。  
  
 **ProductVersion**  
 版本[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]。 最大長度是 15 個字元。 版本號碼的格式應該會如下所示：8.00.0xxx.00。  
  
 **ProductLocaleId**  
 應用程式的 INTL DLL 之地區設定識別碼或語言識別碼 (例如，0x41A)。  
  
 **OperatingSystem**  
 已安裝 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的作業系統。 有效值包括**0**作業系統無關， **1**如[!INCLUDE[win2kfamily](../../../includes/win2kfamily-md.md)]，和**16** Windows xp。  
  
 **CountryLocaleId**  
 作業系統的地區設定識別碼或是語言識別碼。 例如，Windows 法文版本的值為 0x040c。  
  
 **其他相關資訊**  
 包含執行方法時所發生之巢狀運算式的 XML 字串。  
  
 **Source**  
 子項目**MoreInformation**。 錯誤的來源。  
  
 **訊息**  
 子項目**MoreInformation**。 巢狀例外狀況的錯誤訊息。 這個項目包括 XML 屬性**ErrorCode**和**HelpLink**。  
  
 **警告**  
 包含從報表處理傳回之警告的 XML 字串。  
  
## <a name="see-also"></a>另請參閱  
 [例外狀況處理中的 Reporting Services 簡介](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 類別](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [使用詳細資料屬性來處理特定的錯誤](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
