---
title: 指定的資料類型和內容類型 （基本資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 72484d27-3ef1-4f16-813c-2f43231fc2da
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 583a6fda2dbb4698405a3d69f33955531b3c1c10
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62720052"
---
# <a name="specifying-the-data-type-and-content-type-basic-data-mining-tutorial"></a>指定資料類型和內容類型 (基本資料採礦教學課程)
  現在您已經選取用來建立結構及定型模型的資料行，請針對精靈所設定的預設資料類型和內容類型進行任何必要的變更。  
  
#### <a name="review-and-modify-content-type-and-data-type-for-each-column"></a>檢閱及修改每一個資料行的內容類型和資料類型  
  
1.  在 **指定資料行的內容和資料類型**頁面上，按一下**偵測**執行演算法來決定每個資料行的內容類型與預設的資料。  
  
2.  檢閱中的項目**內容的型別**並**資料型別**資料行，並如有必要，請確定設定是以下表所列的相同變更。  
  
     此精靈通常會偵測這些數字並指派適當的數值資料類型，但是在許多情況下，您可能想要將數字當做文字處理。 例如， **GeographyKey**應該當做文字處理，因為它會對此識別碼執行數學運算不恰當。  
  
    |「資料行」|內容類型|資料類型|  
    |------------|------------------|---------------|  
    |**地址行 1**|**不連續**|**Text**|  
    |**地址行 2**|**不連續**|**Text**|  
    |**存留期**|**連續**|**Long**|  
    |**Bike Buyer**|**不連續**|**Long**|  
    |**Commute Distance**|**不連續**|**Text**|  
    |**CustomerKey**|**索引鍵**|**Long**|  
    |**DateLastPurchase**|**連續**|**日期**|  
    |**Email Address**|**不連續**|**Text**|  
    |**English Education**|**不連續**|**Text**|  
    |**English Occupation**|**不連續**|**Text**|  
    |**FirstName**|**不連續**|**Text**|  
    |**Gender**|**不連續**|**Text**|  
    |**地理位置索引鍵**|**不連續**|**Text**|  
    |**House Owner Flag**|**不連續**|**Text**|  
    |**Last Name**|**不連續**|**Text**|  
    |**Marital Status**|**不連續**|**Text**|  
    |**Number Cars Owned**|**不連續**|**Long**|  
    |**Number Children At Home**|**不連續**|**Long**|  
    |**Region**|**不連續**|**Text**|  
    |**Total Children**|**不連續**|**Long**|  
    |**Yearly Income**|**連續**|**Double**|  
  
3.  按一下 [下一步] 。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [為結構指定測試資料集&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/specifying-a-testing-data-set-for-the-structure-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>本課程的前一項工作  
 [建立目標的郵寄採礦模型結構&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [內容類型 &#40;資料採礦&#41;](../../2014/analysis-services/data-mining/content-types-data-mining.md)   
 [資料類型 &#40;資料採礦&#41;](../../2014/analysis-services/data-mining/data-types-data-mining.md)  
  
  
