---
title: "商務規則範例 (Master Data Services) |Microsoft 文件"
ms.custom: 
ms.date: 01/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3974b9be-4b7c-4a37-ab26-1a36ef455744
caps.latest.revision: 21
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 73f7c989b5a2d99f4eb826f2445adddc7bf9d374
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="business-rule-examples-master-data-services"></a>商務規則範例 (Master Data Services)
本文說明 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]的商務規則範例。 您也可以在 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]安裝隨附的範例模型中找到這些範例。   
  
如需如何部署範例模型的指示，請參閱[Master Data Services 安裝和設定](../master-data-services/master-data-services-installation-and-configuration.md)。  
  
  
## <a name="business-rule-examples"></a>商務規則範例  
範例模型 |實體  |商務規則名稱| 說明  
---------|---------|---------|-----------|  
客戶    | 客戶   | 個人付款條件| 指定客戶的預設付款條件。          
在下列商務規則中，如果 CustomerType 屬性值符合 `is equal` [規則條件](../master-data-services/business-rule-conditions-master-data-services.md)，則 `defaults to` [規則動作](../master-data-services/business-rule-conditions-master-data-services.md) 會套用至 PaymentTerms 屬性。 否則，就不採取任何動作。  
```  
If  
    CustomerType is equal to 2  
Then  
    PaymentTerms defaults to CASH  
Else  
    None      
```  
  
**--------------------------------------------------**  
  
範例模型  |實體  |商務規則名稱|說明    
---------|---------|---------|---------------  
客戶     | 客戶    | 組織付款條件 | 指定組織的預設付款條件。         
在下列商務規則中，如果 CustomerType 屬性值符合 `is equal` [規則條件](../master-data-services/business-rule-conditions-master-data-services.md)，則 `defaults to` [規則動作](../master-data-services/business-rule-actions-master-data-services.md) 會套用至 PaymentTerms 屬性。 否則，就不採取任何動作。  
```  
If  
    CustomerType is equal to 1  
Then  
    PaymentTerms defaults to 210Net30  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
範例模型  |實體  |商務規則名稱| 說明    
---------|---------|---------|-----------  
產品     |  產品       | DaysToManufacture |指定製造商的廠內生產天數範圍。          
在下列商務規則中，如果 InHouseManufacture 屬性值符合 `is equal` [規則條件](../master-data-services/business-rule-conditions-master-data-services.md)，則 `must be between` [規則動作](../master-data-services/business-rule-actions-master-data-services.md) 會套用至 DaysToManufacture 屬性。 否則，就不採取任何動作。  
```  
If  
    InHouseManufacture is equal to Y  
Then  
    DaysToManufacture must be between 1 and 10  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
範例模型  |實體  |商務規則名稱|說明    
---------|---------|---------|-------------  
產品     |產品         |必要的欄位| 指定產品實體成員的必要屬性。           
在下列商務規則中，不論何種條件，都會針對指定的屬性採取 `is required` [驗證動作](../master-data-services/business-rule-actions-master-data-services.md) 。 屬性值不能是 Null 或空白。  
```  
If  
    None  
Then  
    Name is required  
    ProductSubCategory is required  
    Color is required  
    StandardCost is required  
    SafetyStockLevel is required  
    ReorderPoint is required  
    InHouseManufacture is required  
    SellStartDate is required  
    FinishedGoodIndicator is required  
    ProductLine is required  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
範例模型  |實體  |商務規則名稱|說明    
---------|---------|---------|-----------  
產品     | 產品        |  標準成本| 標準成本必須大於 0。        
在下列商務規則中，不論何種條件，都會將 `must be greater than` [規則動作](../master-data-services/business-rule-actions-master-data-services.md) 套用到產品的 StandardCost 屬性。  
```  
If  
    None  
Then  
    StandardCost must be greater than 0  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
範例模型  |實體  |商務規則名稱|說明    
---------|---------|---------|------------  
產品     | 產品        | FG MSRP 成本|指定當產品是完好商品時，MSRP (製造商建議的零售價格) 與經銷商成本必須大於 0。           
  
在下列商務規則中，如果 FinishedGoodIndicator 屬性值符合 `is equal` [規則條件](../master-data-services/business-rule-conditions-master-data-services.md)，則 `must be greater than` [規則動作](../master-data-services/business-rule-actions-master-data-services.md) 會套用至 MSRP 和 DealerCost 屬性。  
```  
If  
    FinishedGoodIndicator is equal to Y  
Then  
    MSRP must be greater than 0  
    DealerCost must be greater than 0  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
範例模型  |實體  |商務規則名稱|說明    
---------|---------|---------|------------  
產品     | 產品        |  預設名稱| 依據 Color 和 Class 屬性值指定預設的產品名稱。 當 Color 屬性值不是 YLO 而 Class 屬性值不是 NA 時，預設名稱是 Yellow NA。         
在下列商務規則中，如果不符合的色彩和類別屬性`is equal`規則條件， `defaults to` [規則動作](../master-data-services/business-rule-actions-master-data-services.md)套用到名稱屬性。  
```  
If  
    (Color is equal to YLO AND Class is equal to NA) is not true  
Then  
    Name defaults to Yellow NA  
Else  
    Name defaults to Other  
```  
  
**--------------------------------------------------**  
  
  
**若要檢視範例模型中的商務規則範例**  
1. 瀏覽至 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 網站 (您在安裝 MDS 之後所設定)，然後按一下 [系統管理] 方塊。   
如需設定網站的指示，請參閱[Master Data Services 安裝和設定](../master-data-services/master-data-services-installation-and-configuration.md)。  
2. 按一下含有商務規則的範例模型 (如上述表格所列)，然後按一下 [實體]。  
3. 按一下要套用規則的實體 (如上述表格所列)，然後按一下 [商務規則]。  
4. 按一下您想要檢視的商務規則名稱。 隨即展開 UI 以顯示 **If**、 **Then** 和 **Else** 陳述式。  
  
## <a name="did-this-article-help-you-were-listening"></a>這篇文章對您有幫助嗎？ 我們會持續聽取您的意見   
您要尋找哪些資訊？找到了嗎？ 我們會持續聽取您的意見來改進內容。 請將您的意見傳送到 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com)的商務規則範例。   
  
  
  
  


