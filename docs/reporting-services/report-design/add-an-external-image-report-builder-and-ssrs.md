---
title: 新增外部影像 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 81fd4a1f-79a9-4967-86d6-6229413c0995
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1ac0bc269bfe0b7b443270fcc0eb6bdcc3e09a40
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2019
ms.locfileid: "65582110"
---
# <a name="add-an-external-image-report-builder-and-ssrs"></a>加入外部影像 (報表產生器及 SSRS)
  外部影像可以位於原生模式或 SharePoint 整合模式的報表伺服器上，也可以位於其他任何網站上。 當您在報表中加入外部影像時，您必須確認此影像存在，而且報表讀者有權存取此影像。 如需詳細資訊，請參閱[影像 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-an-external-image"></a>若要加入外部影像  
  
1.  在報表設計檢視的 **[插入]** 索引標籤上，按一下 **[影像]**。  
  
2.  在設計介面上，按一下然後將方塊拖曳至所需的影像大小。  
  
3.  在 **[影像屬性]** 對話方塊的 **[一般]** 索引標籤上，於 **[名稱]** 文字方塊內輸入名稱，或是接受預設值。  
  
4.  (選擇性) 在 [工具提示] 文字方塊中，鍵入您希望使用者將滑鼠停留在轉譯成 HTML 之報表內的影像上方時，所要顯示的文字。  
  
5.  在 **[選取影像來源]** 中，選取 **[外部]**。  
  
     若影像位在處於原生模式的報表伺服器上，請在 [使用此影像] 方塊中鍵入影像的相對路徑，例如 ../images/image1.jpg。  
  
     若影像位在處於 SharePoint 整合模式的報表伺服器或其他任何網站上，請在 [使用此影像] 方塊中鍵入影像的完整 URL，例如 https://\<SharePoint 伺服器名稱>/\<網站>/Documents/images/image1.jpg。  
  
     如需詳細資訊，請參閱[指定外部項目的路徑 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md)。  
  
6.  (選擇性) 按一下 [大小]、[可見度]、[動作] 或 [框線]，為影像報表項目設定其他屬性。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [在報表中內嵌影像 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [加入背景影像 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-a-background-image-report-builder-and-ssrs.md)   
 [影像屬性對話方塊、一般 &#40;報表產生器及 SSRS&#41;](https://msdn.microsoft.com/library/c2218b93-f7fe-46ef-995f-d7dadf9752ec)  
  
  
