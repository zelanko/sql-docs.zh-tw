---
title: Reporting Services SoapException 類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- exceptions [Reporting Services], SoapException class
- SoapException class
ms.assetid: 2cec49ee-20b1-40eb-a75b-0908d9c05b34
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: de33b2cdbc082e609e392d36aa53b8c5bbd2ce4f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48160490"
---
# <a name="reporting-services-soapexception-class"></a>Reporting Services SoapException 類別
  您應該處理可能會發生的特定 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 錯誤。 例如，在您詢問使用者是否建立資料夾的應用程式中，使用者或許會嘗試建立已經存在的資料夾。 身為開發人員，您無法控制使用者在應用程式的資料夾名稱與路徑欄位中輸入的內容，但是，您卻可以控制使用者在試圖建立已經存在的項目時所得到的體驗。  
  
 為了使您更易於捕捉特定的錯誤狀況，[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 會對例外狀況的錯誤碼進行分類，並使用 **SoapException** 類別的屬性傳回錯誤的分類。 如需詳細資訊，請參閱 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK 文件中的＜SoapException 類別＞。  
  
 下表列出 **SoapException** 類別的公用屬性。  
  
|公用屬性|描述|  
|---------------------|-----------------|  
|**Actor**|造成例外狀況的程式碼， 這個值是 Web 服務方法的 URL。|  
|**Detail**|應用程式特定的錯誤資訊， 這個值是由報表伺服器所設定，且格式為 XML。 如需詳細資訊，請參閱 [Detail 屬性](detail-property.md)和[使用 Detail 屬性處理特定的錯誤](../best-practices/using-the-detail-property-to-handle-specific-errors.md)。|  
|**HelpLink**|與該錯誤相關聯的說明檔之 URL 或 URN。 這個值通常是由 Web 服務所設定，而且它會將 URL 設定為 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 說明與支援。 因為 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 對於所發生的錯誤支援多個說明連結，所以報表伺服器會將說明連結資訊設定為 **Detail** 屬性的一部分。 如需詳細資訊，請參閱 [HelpLink 項目](helplink-element.md)。|  
|**Message**|描述錯誤的當地語系化描述性訊息。 此文字可能會出現在應用程式 UI 中。|  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 中的例外狀況處理簡介](../introducing-exception-handling-in-reporting-services.md)   
 [SoapException 錯誤資料表](soapexception-errors-table.md)  
  
  
