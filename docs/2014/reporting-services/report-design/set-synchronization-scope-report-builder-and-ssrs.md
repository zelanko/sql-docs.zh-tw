---
title: 設定同步處理範圍 （報表產生器及 SSRS） |Microsoft 文件
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 6f4a11e6-6151-47be-a43f-e3dbf6c0e737
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 69fa6500439e51705e9dfd3ee838c2f7e1b4eddb
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66105000"
---
# <a name="set-synchronization-scope-report-builder-and-ssrs"></a>設定同步處理範圍 (報表產生器及 SSRS)
  指標會在指定的範圍內，跨指標值的範圍進行同步處理，藉以傳達資料值。 根據預設，此範圍是指標的父容器，例如，包含指標的資料表或矩陣。 您可以根據報表的版面配置來變更指標的同步處理。 例如，如果某個資料表之類的資料區有資料列群組，您可以將群組指定為指標範圍。 指標也可以省略同步處理。  
  
 您可以使用運算式來設定選項，如度量單位。 如需詳細資訊，請參閱[運算式 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)。  
  
 如需了解和設定報表內範圍的一般資訊，請參閱[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-synchronization-scope-of-an-indicator"></a>若要變更指標的同步處理範圍  
  
1.  以滑鼠右鍵按一下您要變更的指標，然後按一下 **[指標屬性]**。  
  
2.  按一下左窗格中的 **[值和狀態]** 。  
  
3.  在 **[同步處理範圍]** 清單中，按一下您要套用的範圍。  
  
     [(無)] 選項 (會從指標移除同步處理範圍) 永遠可以使用。 其他選項則取決於您報表的版面配置。  
  
     或者，按一下 [運算式]\(*fx*) 按鈕來編輯設定範圍的運算式。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [指標 &#40;報表產生器及 SSRS&#41;](indicators-report-builder-and-ssrs.md)  
  
  
