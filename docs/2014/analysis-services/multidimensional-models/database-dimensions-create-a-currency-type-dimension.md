---
title: 建立貨幣類型維度 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- dimensions [Analysis Services], currency
- currency [Analysis Services]
- converting currency
- currency dimensions [Analysis Services]
ms.assetid: b1f037d1-ce47-4e47-a1c2-5ec9e781cff6
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f45683b404e9a33260edda6163aae9f783c8b7f4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030175"
---
# <a name="create-a-currency-type-dimension"></a>建立貨幣類型維度
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，貨幣類型維度是指其屬性代表財務報表所使用之貨幣清單的維度。  
  
 貨幣維度可讓您將貨幣轉換功能加入至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的 Cube 中。 若要將貨幣轉換加入至 Cube，您可以使用商業智慧精靈定義多維度運算式 (MDX) 指令碼命令，將貨幣量值轉換成適合用戶端應用程式地區設定的值。 若要建立這個 MDX 指令碼，商業智慧精靈需要下列資訊：  
  
-   代表來源貨幣的貨幣維度。 (此維度是來源貨幣維度)。  
  
-   代表要使用之匯率的量值群組。  
  
 商業智慧精靈可利用此資訊設計一個貨幣轉換程序，來識別適當的目的地貨幣維度 (代表目的地貨幣的貨幣維度)。 視商業智慧方案需要的貨幣轉換數目而定，商業智慧精靈可定義多個目的地貨幣維度。 如需定義貨幣轉換的詳細資訊，請參閱[貨幣轉換 &#40;Analysis Services&#41;](../currency-conversions-analysis-services.md)。  
  
 若要將維度識別為貨幣維度，設定`Type`屬性的維度`Currency`。  
  
## <a name="dimension-structure"></a>維度結構  
 貨幣維度會包含至少一個索引鍵屬性，來識別貨幣維度之維度資料表中的個別貨幣。 在來源和目的地貨幣維度中，索引鍵屬性的值是不同的：  
  
-   若要將屬性識別為來源貨幣維度的索引鍵屬性，請將該屬性的 `Type` 屬性設定為 `CurrencySource`。  
  
-   若要將屬性識別為目的地貨幣維度，設定`Type`將屬性的屬性`CurrencyDestination`。  
  
 基於報表用途，來源和目的地貨幣維度都可選擇性地包含下列屬性：  
  
-   貨幣名稱屬性。  
  
     若要將屬性識別為貨幣名稱屬性，請將屬性的 `Type` 屬性設定為 `CurrencyName`。  
  
-   貨幣來源屬性。  
  
     若要將屬性識別為貨幣來源屬性，請將屬性的 `Type` 屬性設定為 `CurrencySource`。  
  
-   貨幣國際標準組織 (ISO) 代碼。  
  
     若要將屬性識別為貨幣 ISO 代碼屬性，設定`Type`將屬性的屬性`CurrencyIsoCode`。  
  
 如需屬性類型的詳細資訊，請參閱 [設定屬性類型](attribute-properties-configure-attribute-types.md)。  
  
## <a name="defining-account-intelligence-with-the-business-intelligence-wizard"></a>使用商業智慧精靈定義帳戶智慧  
 在定義帳戶維度並將該維度加入至 Cube 之後，您就可以使用商業智慧精靈來加入帳戶智慧功能，例如識別及對應帳戶類型至維度。 如需詳細資訊，請參閱[將帳戶智慧加入至維度中](bi-wizard-add-account-intelligence-to-a-dimension.md)。  
  
## <a name="see-also"></a>另請參閱  
 [屬性和屬性階層](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [商業智慧精靈 F1 說明](../business-intelligence-wizard-f1-help.md)   
 [維度類型](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  