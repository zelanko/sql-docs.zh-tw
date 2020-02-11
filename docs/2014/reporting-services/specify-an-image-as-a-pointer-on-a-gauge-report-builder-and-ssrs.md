---
title: 將影像指定為量測計的指標（報表產生器及 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 9d73b3c3-a068-4868-a2be-0cd261b6e92b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c7a57987a5d1cd0ac7984db3b716521d9c7a09af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66101151"
---
# <a name="specify-an-image-as-a-pointer-on-a-gauge-report-builder-and-ssrs"></a>將影像指定為量測計的指標 (報表產生器及 SSRS)
  量測計包含三個內建樣式，可用來自訂指標的外觀。 星形量測計的內建樣式如下：指針、標記和列。 線性量測計的內建樣式如下：標記、列和溫度計。 如果需要唯一的指標，使用者可以建立並指定可當做完整功能之指標使用的影像。  
  
 當您指定指標的影像時，影像必須具有下列規格：  
  
-   指標的原點或旋轉的中心必須位於影像的頂端。  
  
-   指標的結尾必須指向下方。  
  
 因為指標是不規則的形狀，所以您必須指定透明色彩來隱藏指標的不必要部分。 由於指定的色彩不會顯示在量測計上，因此請考慮使用通常不會顯示在量測計上的色彩當做透明色彩。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-an-image-as-a-pointer-on-the-gauge"></a>將影像指定為量測計的指標  
  
1.  在 [設計] 檢視中，按一下量測計的指標。  
  
2.  選擇性如果量測計上沒有指標存在，請以滑鼠右鍵按一下量測計，然後選取 [**加入指標**]。 指標就會加入至量測計。  
  
3.  按一下功能區上的 [**插入**] 索引標籤，然後按兩下影像圖示。 [影像屬性]**** 對話方塊隨即開啟。  
  
4.  將影像加入至報表。 如需詳細資訊，請參閱[在報表中內嵌影像 &#40;報表產生器和 SSRS&#41;](report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)。  
  
5.  開啟 [屬性] 窗格。  
  
6.  在設計介面上按一下指標。 指標的屬性就會顯示在 [屬性] 窗格中。  
  
7.  展開 [PointerImage] 節點。  
  
8.  在 [**來源**] 中，從下拉式清單中選取 [**內嵌**]。  
  
    > [!NOTE]  
    >  如果您的影像儲存在資料庫中或網路上，可以針對此屬性指定適當的選項。 如需詳細資訊，請參閱[影像屬性對話方塊、一般 &#40;報表產生器和 SSRS&#41;](../../2014/reporting-services/image-properties-dialog-box-general-report-builder-and-ssrs.md)。  
  
9. 在 [**值**] 中，從下拉式清單中選取您的映射名稱。  
  
10. 在 [ **TransparentColor**] 中，挑選您想要從影像中移除的色彩值。 這樣就會針對量測計的指標建立連續的外觀。  
  
## <a name="see-also"></a>另請參閱  
 [格式化量測計上的指標 &#40;報表產生器及 SSRS&#41;](report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [將量測計加入報表 &#40;報表產生器和 SSRS&#41;](report-design/add-a-gauge-to-a-report-report-builder-and-ssrs.md)   
 [格式化線條、色彩和影像 &#40;報表產生器及 SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [量測計 &#40;報表產生器及 SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md)  
  
  
