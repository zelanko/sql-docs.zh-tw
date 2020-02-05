---
title: 在 URL 內傳遞報表參數 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services], passing parameters
- passing parameters [Reporting Services]
ms.assetid: f93a94cc-27b5-435a-aa85-69e6ec6459ad
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 551fc19b3d39ef6cf12c5fdd4e77196b0abbb9fe
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "65580833"
---
# <a name="pass-a-report-parameter-within-a-url"></a>在 URL 內傳遞報表參數
  您可以在報表 URL 中包括報表參數，以便將它們傳遞給報表。 這些 URL 參數不會加上前置詞，因為它們會直接傳遞給報表處理引擎。  

> [!NOTE]
> SQL Server 2016 後即不再提供 Reporting Services 與 SharePoint 的整合。
  
> [!IMPORTANT]  
>  請務必讓 URL 包含 `_vti_bin` Proxy 語法，以便透過 SharePoint 和 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] HTTP Proxy 路由傳送要求。 此 Proxy 會將某些內容加入至 HTTP 要求，也就是確保針對 SharePoint 模式報表伺服器正確執行報表所需的內容。  
>   
>  如果您未包含 Proxy 語法，則需要為參數加上前置詞 *rp:* 。  
  
 所有查詢參數都可以有相對應的報表參數。 您可以傳遞相對應的報表參數，即可傳遞查詢參數。 如需詳細資訊，請參閱[在關聯式查詢設計工具中建立查詢 &#40;報表產生器和 SSRS&#41;](../reporting-services/report-data/build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md)。  
  
> [!IMPORTANT]
>  報表參數會區分大小寫。  
> 
> [!NOTE]
>  報表參數會區分大小寫，而且使用下列特殊字元：  
> 
>  -   根據 URL 編碼標準，在 URL 字串中的任何空格字元都會使用字元 "%20" 來取代。  
> -   URL 參數部分中的空格字元會取代成加號字元 (+)。  
> -   任何字串部分中的分號都會取代成 "%3A" 字元。  
> -   瀏覽器應該會自動執行正確的 URL 編碼。 您不必手動編碼任何字元。  
  
 若要設定 URL 內的報表參數，請使用以下語法：  
  
```  
  
parameter=value  
```  
  
 例如，若要指定兩個定義在報表中的參數 ("ReportMonth" 和 'ReportYear")，請使用下列原生模式報表伺服器的 URL：  
  
```  
https://myrshost/ReportServer?/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2&ReportMonth=3&ReportYear=2008  
```  
  
 例如，若要指定定義在報表中的兩個相同參數，請將下列 URL 用於 SharePoint 整合模式報表伺服器。 請注意 `/_vti_bin`：  
  
```  
https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2.rdl&ReportMonth=3&ReportYear=2008  
```  
  
 若要為參數傳遞 Null 值，請使用下列語法：  
  
```  
  
parameter  
:isnull=true  
  
```  
  
 例如，  
  
```  
SalesOrderNumber:isnull=true  
```  
  
 若要傳遞 **布林** 值，請使用 0 表示 False，使用 1 表示 True。 若要傳遞 **浮點數** 值，請包含伺服器地區設定的小數分隔符號  
  
> [!NOTE]  
>  如果報表中包含具有預設值的報表參數，而且 **Prompt** 屬性的值是 **false** (也就是在報表管理員中未選取 [提示使用者] 屬性)，則您無法在 URL 內傳遞該報表參數的值。 這可讓管理員選擇防止使用者加入或修改某些報表參數值。  
  
##  <a name="bkmk_examples"></a> 其他範例  
 下列 URL 範例包含空格和多個參數。  
  
-   資料夾名稱 "SQL Server User Education Team" 包含空格，因此 "+" 會取代每個空格。  
  
-   "team project report" 的報表名稱包含空格，因此 "+" 會取代每個空格。  
  
-   傳遞兩個參數："teamgrouping2" 的值為 "xgroup"，"teamgrouping1" 的值為 "ygroup"。  
  
```  
https://myserver/Reportserver?/SQL+Server+User+Education+Team/_ContentTeams/folder123/team+project+report&teamgrouping2=xgroup&teamgrouping1=ygroup  
```  
  
 下列 URL 範例包含多值參數 "OrderID"。 多值參數的格式是針對每個值重複參數名稱。  
  
```  
https://myserver/Reportserver?/SQL+Server+User+Education+Team/_ContentTeams/folder123/team+project+report&teamgrouping2=xgroup&teamgrouping1=ygroup&OrderID=747&OrderID=787&OrderID=12  
```  
  
 下列 URL 範例會針對原生模式報表伺服器傳遞具有值 "7/1/2005" 的單一參數 *SellStartDate*。  
  
```  
https://myserver/ReportServer/Pages/ReportViewer.aspx?%2fProduct_and_Sales_Report_AdventureWorks&SellStartDate=7/1/2005  
```  
  
## <a name="see-also"></a>另請參閱  
 [URL 存取 &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [URL 存取參數參考](../reporting-services/url-access-parameter-reference.md)  
  
  
