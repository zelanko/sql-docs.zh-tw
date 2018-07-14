---
title: 新增外部影像 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 81fd4a1f-79a9-4967-86d6-6229413c0995
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 16caea1e5b4eafa9a5774ba5ca7476df16406f0d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37268524"
---
# <a name="add-an-external-image-report-builder-and-ssrs"></a>加入外部影像 (報表產生器及 SSRS)
  外部影像可以位於原生模式或 SharePoint 整合模式的報表伺服器上，也可以位於其他任何網站上。 當您在報表中加入外部影像時，您必須確認此影像存在，而且報表讀者有權存取此影像。 如需詳細資訊，請參閱[影像 &#40;報表產生器及 SSRS&#41;](images-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-an-external-image"></a>若要加入外部影像  
  
1.  在報表設計檢視的 **[插入]** 索引標籤上，按一下 **[影像]**。  
  
2.  在設計介面上，按一下然後將方塊拖曳至所需的影像大小。  
  
3.  在 **[影像屬性]** 對話方塊的 **[一般]** 索引標籤上，於 **[名稱]** 文字方塊內輸入名稱，或是接受預設值。  
  
4.  (選擇性) 在 [工具提示] 文字方塊中，鍵入您希望使用者將滑鼠停留在轉譯成 HTML 之報表內的影像上方時，所要顯示的文字。  
  
5.  在 **[選取影像來源]** 中，選取 **[外部]**。  
  
     若為處於原生模式之報表伺服器上的影像，請在 [使用此影像] 方塊中輸入影像的相對路徑，例如 ../images/image1.jpg。  
  
     若為處於 SharePoint 整合模式之報表伺服器或其他任何網站上的影像，請在 [使用此影像] 方塊中鍵入影像的完整 URL，例如 http://\<SharePoint 伺服器名稱>/\<網站>/Documents/images/image1.jpg。  
  
     如需詳細資訊，請參閱[指定外部項目的路徑 &#40;報表產生器及 SSRS&#41;](specifying-paths-to-external-items-report-builder-and-ssrs.md)。  
  
6.  (選擇性) 按一下 [大小]、[可見度]、[動作] 或 [框線]，為影像報表項目設定其他屬性。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [將影像內嵌在報表中&#40;報表產生器及 SSRS&#41;](embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [新增背景影像 &#40;報表產生器及 SSRS&#41;](add-a-background-image-report-builder-and-ssrs.md)   
 [影像屬性對話方塊、一般 &#40;報表產生器及 SSRS&#41;](../image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
