---
title: 新增或刪除指標 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: a8b1aac1-53ef-47a4-afc0-8fa866c6c480
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a3bea101bf16376ffc02699dc700f500f08f7222
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56017719"
---
# <a name="add-or-delete-an-indicator-report-builder-and-ssrs"></a>加入或刪除指標 (報表產生器及 SSRS)
  指標是最小的量測計，看一眼就可傳達單一資料值的狀態。 如需指標的詳細資訊，請參閱[指標 &#40;報表產生器及 SSRS&#41;](indicators-report-builder-and-ssrs.md)。  
  
 指標通常會放在資料表或矩陣的資料格中，但是您也可以單獨使用指標、與量測計並存使用，或是內嵌在量測計中。  
  
 當您初次加入指標時，預設會將它設定為使用百分比做為度量單位。 百分比範圍會平均分佈在指標集合的成員當中，而且指標顯示的值範圍為指標的父項，例如資料表或矩陣。  
  
 您可以更新指標的值和狀態。 如需詳細資訊，請參閱下列主題：  
  
-   [變更指標圖示和指標集合 &#40;報表產生器及 SSRS&#41;](change-indicator-icons-and-indicator-sets-report-builder-and-ssrs.md)  
  
-   [設定度量單位 &#40;報表產生器及 SSRS&#41;](set-and-configure-measurement-units-report-builder-and-ssrs.md)  
  
-   [設定同步處理範圍 &#40;報表產生器及 SSRS&#41;](set-synchronization-scope-report-builder-and-ssrs.md)  
  
 因為指標位於量測計面板的內部，所以當您想要使用 [指標屬性] 對話方塊或 [屬性] 窗格來設定指標時，您需要選取指標，而不是此面板。 下圖顯示選取的指標如何出現在它的量測計面板中。  
  
 ![rs_GaugePanelWithIndicator](../media/rs-gaugepanelwithindicator.gif "rs_GaugePanelWithIndicator")  
  
> [!NOTE]  
>  根據資料值的資料行寬度和長度，資料表或矩陣資料格中的文字可能會換行，並將文字顯示在多行上。 發生這個情況時，指標圖示可能會伸展並變更形狀。 這可能會使指標圖示較不容易讀取。 將指標放在矩形內部以確認圖示絕不會伸展。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-an-indicator-to-a-table-or-matrix"></a>若要將指標加入至資料表或矩陣  
  
1.  開啟現有的報表，或建立新的報表，其中包含的資料表和矩陣含有您想要顯示的資料。 如需詳細資訊，請參閱[資料表 &#40;報表產生器及 SSRS&#41;](tables-report-builder-and-ssrs.md) 和[矩陣 &#40;報表產生器及 SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)。  
  
2.  將資料行插入資料表或矩陣中。 如需詳細資訊，請參閱[插入或刪除資料行 &#40;報表產生器及 SSRS&#41;](insert-or-delete-a-column-report-builder-and-ssrs.md)。  
  
3.  選擇性地在 [插入] 索引標籤上，按一下 [矩形]，然後在新的資料行中按一下資料格。  
  
4.  在 [插入] 索引標籤上，按一下 [指標]，然後在新的資料行中按一下資料格。  
  
     如果您已經將矩形加入至資料格，按一下該資料格。  
  
5.  在左窗格的 [Select Indicator Style] (選取指標樣式) 對話方塊中，按一下您想要的指標類型，然後按一下指標集合。  
  
6.  按一下 [確定] 。  
  
7.  按一下指標。 [量測計資料] 窗格隨即開啟。  
  
8.  在 [值] 區域的 [(未指定)] 下拉式清單中，按一下您希望其值顯示為指標的欄位。  
  
     指標會設定為使用預設值。 根據預設，指標會設定為使用百分比當做度量單位，而且百分比範圍會平均分佈在指標的成員當中，而指標傳達的值會使用最近的群組範圍。  
  
### <a name="to-delete-an-indicator-to-a-table-or-matrix"></a>若要刪除資料表或矩陣中的指標  
  
1.  以滑鼠右鍵按一下要刪除的指標，然後按一下 [刪除]。  
  
    > [!NOTE]  
    >  指標可能會位於包含其他指標或量測計的量測計面板內部。 如果量測計面板包含多個項目，請務必按一下指標來將它刪除，而不是按一下量測計面板。 如果您按一下並刪除量測計面板，量測計面板以及其中的所有項目都會遭到刪除。  
  
2.  按一下 **[刪除]**。  
  
## <a name="see-also"></a>另請參閱  
 [指標 &#40;報表產生器及 SSRS&#41;](indicators-report-builder-and-ssrs.md)  
  
  
