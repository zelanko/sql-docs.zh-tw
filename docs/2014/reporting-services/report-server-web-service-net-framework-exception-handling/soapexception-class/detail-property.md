---
title: 詳細資料屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- Detail property
- SoapException class
ms.assetid: c1ddaeb6-c540-49fa-b06e-b6359d377ee8
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 383e356a85597a6b6564584fc375e83f258241b9
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56019357"
---
# <a name="detail-property"></a>詳細資料屬性
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] **SoapException** 類別的 **Detail** 屬性具有下列 XML 結構：  
  
## <a name="elements"></a>元素  
 **Detail**  
 包含所有其他錯誤詳細資料元素的上層元素。  
  
 **ErrorCode**  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 特定的錯誤碼。  
  
 **HttpStatus**  
 HTTP 狀態碼。  
  
 **Message**  
 報表伺服器指派的錯誤訊息與錯誤碼。  
  
 **HelpLink**  
 網站的說明連結 URL，在此可以找到有關錯誤的進一步資訊。 如需詳細資訊，請參閱 [HelpLink 項目](helplink-element.md)。  
  
 **LinkID**  
 指派給該連結的識別碼。  
  
 **ProductName**  
 產品的名稱。 預設值是 **Microsoft SQL Server Reporting Services**。  
  
 **ProductVersion**  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的版本。 最大長度是 15 個字元。 版本號碼的格式應該如下所示：8.00.0xxx.00。  
  
 **ProductLocaleId**  
 應用程式的 INTL DLL 之地區設定識別碼或語言識別碼 (例如，0x41A)。  
  
 **OperatingSystem**  
 已安裝 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 的作業系統。 與作業系統無關時，有效值為 **0**，[!INCLUDE[win2kfamily](../../../includes/win2kfamily-md.md)] 為 **1**，而 Windows XP 則為 **16**。  
  
 **CountryLocaleId**  
 作業系統的地區設定識別碼或是語言識別碼。 例如，Windows 法文版本的值為 0x040c。  
  
 **MoreInformation**  
 包含執行方法時所發生之巢狀運算式的 XML 字串。  
  
 **Source**  
 **MoreInformation** 的子項目。 錯誤的來源。  
  
 **Message**  
 **MoreInformation** 的子項目。 巢狀例外狀況的錯誤訊息。 這個項目包括 **ErrorCode** 與 **HelpLink** 的 XML 屬性。  
  
 **警告**  
 包含從報表處理傳回之警告的 XML 字串。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 中的例外狀況處理簡介](../introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException 類別](reporting-services-soapexception-class.md)   
 [使用 Detail 屬性來處理特定的錯誤](../best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
