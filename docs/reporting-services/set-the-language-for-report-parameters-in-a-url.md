---
title: "在 URL 中的報表參數設定的語言 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- overriding report language settings
- report servers [Reporting Services], language settings
- languages [Reporting Services]
- URL access [Reporting Services], language overrides
- international considerations [Reporting Services]
- global considerations [Reporting Services]
ms.assetid: e1ccf22f-80d6-45bc-aae0-f5f263275092
caps.latest.revision: 29
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 815af671e5bd26445153b96f68ebcbaf0e972cf7
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="set-the-language-for-report-parameters-in-a-url"></a>設定 URL 中報表參數的語言
  *rs:ParameterLanguage* URL 存取參數會緩和問題，其中區分文化特性的報表參數 (例如、日期、時間、貨幣和數字) 會使用瀏覽器語言進行解譯。 透過 *rs:ParameterLanguage*，現在可以獨立於瀏覽器之外解譯 URL。 例如，如果將報表伺服器設定為德文的區域設定，但是使用者是透過使用設定為英文 (美國) 的瀏覽器之 URL 來存取報表，則傳遞到報表伺服器的參數值將會被誤解。  
  
 請考慮下列存取報表的 URL：  
  
```  
http://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008  
```  
  
 在上述情況中，在 "de-de" 的文化特性之下執行的伺服器，會透過電子郵件訂閱或是超連結產生 URL。 超連結指出報表應該根據德文的日期/時間標準，以 2008 年 10 月 4 日的開始日期與 2008 年 10 月 11 日的結束日期來參數化。 不過，透過設定為 "en-us" 的瀏覽器來存取 URL 的使用者，會強制伺服器在美國英文日期/時間的標準之下，將值解譯為 2008 年 4 月 10 日與 2008 年 11 月 10 日。 若要修正問題， *rs:ParameterLanguage* 可用以覆寫用於參數解譯的瀏覽器語言：  
  
```  
http://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008&rs:ParameterLanguage=de-DE  
```  
  
 除了 URL 存取參數 **rc:Parameters** 的 **true** 和 *false*值之外，您現在可以傳遞 **Collapsed**的值。 在 URL 上使用 *rc:Parameters*=**Collapsed** 時，會摺疊 HTML 檢視器的參數提示區域使其看不到，但是使用者仍然可以切換它。 值為 **false** 時，會從 HTML 檢視器工具列移除參數提示區域，並使其無法供使用者使用。  
  
## <a name="see-also"></a>請參閱＜  
 [URL 存取 &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [URL 存取參數參考](../reporting-services/url-access-parameter-reference.md)  
  
  
