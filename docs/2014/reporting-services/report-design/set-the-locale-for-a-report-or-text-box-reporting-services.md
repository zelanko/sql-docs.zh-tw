---
title: 設定報表或文字方塊的地區設定 (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- locales [Reporting Services]
ms.assetid: df115b01-184b-47f0-b5ec-0ad965ff9bee
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 03f99854aff2333bdb01387d07c90f81c98abe76
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56285236"
---
# <a name="set-the-locale-for-a-report-or-text-box-reporting-services"></a>設定報表或文字方塊的地區設定 (Reporting Services)
  報表或文字方塊上的 **[Language]** 屬性包含地區設定，地區設定會決定用來顯示依語言和地區而不同之報表資料的預設格式，例如日期、貨幣或數值。 文字方塊上的 **[Language]** 屬性會覆寫報表上的 **[Language]** 屬性。 如果 **[Language]** 未指定任何值，Reporting Services 會針對發行的報表使用報表伺服器上作業系統的地區設定，或是針對報表預覽使用報表撰寫電腦的地區設定。  
  
 如果是 HTML 報表，您可以覆寫預設的 **Language** 值，並使用瀏覽器用戶端之 HTTP 標頭所指定的語言，其方式是在報表或文字方塊之 **Language** 屬性的運算式內使用內建的 User!Language 欄位。  
  
 您也可以在 URL 中指定報表的 **[Language]** 屬性。 如需詳細資訊，請參閱 [設定 URL 中報表參數的語言言](../set-the-language-for-report-parameters-in-a-url.md)。  
  
### <a name="to-set-the-locale-for-a-report"></a>若要設定報表的地區設定  
  
1.  在 [設計] 檢視中，按一下報表設計介面的外面來選取報表。  
  
2.  在 [屬性] 窗格中，針對 **[Language]** 屬性輸入或選取您要用於報表的語言。  
  
### <a name="to-set-the-locale-for-a-text-box"></a>若要設定文字方塊的地區設定  
  
1.  在 [設計] 檢視中，選取要套用地區設定的文字方塊。  
  
2.  在 [屬性] 窗格中執行下列動作：  
  
    -   針對 **[Calendar]** 屬性，請輸入或選取用於日期的日曆。  
  
    -   針對 **[Direction]** 屬性，輸入或選取文字的書寫方向。  
  
    -   針對 **[Language]** 屬性，請輸入或選取要用於文字方塊的語言。 這個值會覆寫報表的 **[Language]** 屬性。  
  
    -   針對 **[NumeralLanguage]** 屬性，請輸入或選取文字方塊中所使用的數字格式。  
  
    -   針對 **[NumeralVariant]** 屬性，輸入或選取文字方塊中所使用之數字格式的變數。  
  
    -   針對 **[UnicodeBiDi]** 屬性，選取文字方塊中所使用之雙向內嵌的層級。  
  
## <a name="see-also"></a>另請參閱  
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)  
  
  
