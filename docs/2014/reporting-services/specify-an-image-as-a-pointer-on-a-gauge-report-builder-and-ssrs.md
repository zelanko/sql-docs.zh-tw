---
title: 將影像指定為指標，以量測計 （報表產生器及 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9d73b3c3-a068-4868-a2be-0cd261b6e92b
caps.latest.revision: 7
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d96efa70219c841abae8d0129716810645d283d1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37230138"
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
  
2.  （選擇性）如果在量測計上不存在任何指標，以滑鼠右鍵按一下量測計，然後選取**加入指標**。 指標就會加入至量測計。  
  
3.  按一下 **插入**功能區上索引標籤，然後按兩下影像圖示。 [影像屬性] 對話方塊隨即開啟。  
  
4.  將影像加入至報表。 如需詳細資訊，請參閱 <<c0> [ 將影像內嵌在報表中&#40;報表產生器及 SSRS&#41;](report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)。</c0>  
  
5.  開啟 [屬性] 窗格。  
  
6.  在設計介面上按一下指標。 指標的屬性就會顯示在 [屬性] 窗格中。  
  
7.  展開 PointerImage 節點。  
  
8.  在 **來源**，選取**內嵌**從下拉式清單。  
  
    > [!NOTE]  
    >  如果您的影像儲存在資料庫中或網路上，可以針對此屬性指定適當的選項。 如需詳細資訊，請參閱 <<c0> [ 影像屬性對話方塊、 一般&#40;報表產生器及 SSRS&#41;](../../2014/reporting-services/image-properties-dialog-box-general-report-builder-and-ssrs.md)。</c0>  
  
9. 在 **值**，從下拉式清單中選取您的映像的名稱。  
  
10. 在  **transparentcolor**，挑選您想要移除映像中的色彩值。 這樣就會針對量測計的指標建立連續的外觀。  
  
## <a name="see-also"></a>另請參閱  
 [格式化量測計上的指標 &#40;報表產生器及 SSRS&#41;](report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [將量測計加入至報表&#40;報表產生器及 SSRS&#41;](report-design/add-a-gauge-to-a-report-report-builder-and-ssrs.md)   
 [格式化線條、色彩和影像 &#40;報表產生器及 SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [量測計 &#40;報表產生器及 SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md)  
  
  
