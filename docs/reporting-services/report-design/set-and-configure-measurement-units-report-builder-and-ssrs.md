---
title: 設定度量單位 (報表產生器) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: a15a96c3-7d2c-433e-a440-4ea051e967a9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7651373c21b2e22d88a11d196e3f5c0322b07fe0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "77081019"
---
# <a name="set-and-configure-measurement-units-report-builder-and-ssrs"></a>設定度量單位 (報表產生器及 SSRS)
  在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分頁報表中，指標使用下列兩個度量單位的其中一個︰百分比或數值。   
    
  根據預設，指標會設定為使用百分比做為度量單位。 也就是說，指派給指標集合中每個圖示的指標值取決於百分比範圍。 百分比範圍會在指標集合的圖示中平均分配。 每個圖示代表一個指標狀態。 您可以指定不同的開始與結束百分比來變更指標集合中每個圖示的百分比。 指標也會自動偵測資料中的最小值與最大值。  
  
 您可以將度量單位變更為數值。 在此情況下，您不用指定資料的最小值與最大值；您只要為每個圖示提供指標所使用的開始值與結束值即可。  
  
 您可以使用運算式來設定選項，如度量單位。 如需詳細資訊，請參閱[運算式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)。  
  
## <a name="to-use-the-numeric-state-measurement-unit"></a>若要使用數值狀態度量單位  
  
1.  以滑鼠右鍵按一下您要變更的指標，然後按一下 [指標屬性]  。  
  
2.  按一下左窗格中的 **[值和狀態]** 。  
  
3.  在 [狀態度量單位]  清單中，按一下 [數值]  。  
  
     您可以選擇按一下 [運算式]  \(*fx*) 按鈕來編輯設定選項值的運算式。  
  
4.  針對指標集合中的每個圖示，更新 [開始]  與 [結束]  文字方塊中的值。  
  
     您可以選擇按一下 [運算式]  \(*fx*) 按鈕來編輯設定 [開始]  和 [結束]  選項值的運算式。  
  
    > [!NOTE]  
    >  [開始]  和 [結束]  文字方塊中的值必須是數值。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-use-the-percentage-measurement-unit"></a>若要使用百分比度量單位  
  
1.  以滑鼠右鍵按一下您要變更的指標，然後按一下 [指標屬性]  。  
  
2.  按一下左窗格中的 **[值和狀態]** 。  
  
3.  在 [狀態度量單位]  清單中，按一下 [百分比]  。  
  
     您可以選擇按一下 [運算式]  \(*fx*) 按鈕來編輯設定選項值的運算式。  
  
4.  或者，變更 [最小值]  與 [最大值]  選項來使用特定的值，而非自動偵測指標所使用之資料的最小值與最大值。 [最小值]  的值必須小於 [最大值]  的值。  
  
    > [!NOTE]  
    >  如果您明確地設定最小值和最大值，不論資料中實際的最小值和最大值為何，指標都會使用該值範圍。 也就是說，小於最小值且大於最大值的值會排除在決定報表中顯示之指標圖示的評估之外。  
  
     您可以選擇按一下 [運算式]  \(*fx*) 按鈕來編輯設定選項值的運算式。  
  
5.  針對指標集合中的每個圖示，更新 [開始]  與 [結束]  文字方塊中的值。  
  
     您可以選擇按一下 [運算式]  \(*fx*) 按鈕來編輯設定 [開始]  和 [結束]  選項值的運算式。  
  
    > [!NOTE]  
    >  [開始]  和 [結束]  文字方塊中的值必須是數值。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [指標 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
