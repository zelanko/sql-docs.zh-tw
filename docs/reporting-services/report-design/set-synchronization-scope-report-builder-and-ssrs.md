---
title: 設定同步處理範圍 (報表產生器) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 6f4a11e6-6151-47be-a43f-e3dbf6c0e737
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b5c844bf2ad09ee29dbcda1773e20d93eeb069d1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "77081014"
---
# <a name="set-synchronization-scope-report-builder-and-ssrs"></a>設定同步處理範圍 (報表產生器及 SSRS)
  在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分頁報表中，指標會在指定的範圍內，跨指標值的範圍進行同步處理，藉以傳達資料值。   
    
  根據預設，此範圍是指標的父容器，例如，包含指標的資料表或矩陣。 您可以根據報表的版面配置來變更指標的同步處理。 例如，如果某個資料表之類的資料區有資料列群組，您可以將群組指定為指標範圍。 指標也可以省略同步處理。  
  
 您可以使用運算式來設定選項，如度量單位。 如需詳細資訊，請參閱[運算式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)。  
  
 如需了解和設定報表內範圍的一般資訊，請參閱[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="to-change-the-synchronization-scope-of-an-indicator"></a>若要變更指標的同步處理範圍  
  
1.  以滑鼠右鍵按一下您要變更的指標，然後按一下 [指標屬性]  。  
  
2.  按一下左窗格中的 **[值和狀態]** 。  
  
3.  在 **[同步處理範圍]** 清單中，按一下您要套用的範圍。  
  
     [(無)]  選項 (會從指標移除同步處理範圍) 永遠可以使用。 其他選項則取決於您報表的版面配置。  
  
     或者，按一下 [運算式]  \(*fx*) 按鈕來編輯設定範圍的運算式。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [指標 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
