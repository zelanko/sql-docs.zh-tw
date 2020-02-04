---
title: 變更資料格內的項目 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 91a54778-8929-41f9-bb4c-826cec636be4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cc13f82453349b16e4c9fc00b8f0f083652daa75
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "65581742"
---
# <a name="change-an-item-within-a-cell-report-builder-and-ssrs"></a>變更資料格內的項目 (報表產生器及 SSRS)
在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分頁報表中，只有非容器項目 (例如文字方塊、線條或影像) 才能以新報表項目來取代。 例如，您可以將資料表拖曳到文字方塊，即可以資料表取代文字方塊。  
  
 如果資料格含有矩形、清單、資料表或矩陣等容器項目，就會將新項目加入至包含項目中而非取代它。 若要以新的項目取代容器，請刪除此容器。 刪除容器項目會以文字方塊來取代它，然後您可以用其他項目來取代此文字方塊。  
  
 根據預設，資料表、矩陣或清單資料區內的所有資料格都有包含文字方塊。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-change-an-item-within-a-cell"></a>若要變更資料格內的項目  
  
-   在 **[插入]** 索引標籤的 **[資料區域]** 或 **[報表項目]** 群組中，按一下您想要加入至報表的項目，然後按一下報表。 如此項目就會加入至報表。  
  
> [!NOTE]  
>  當您將影像報表項目拖曳至資料格時，[影像屬性]  對話方塊即會開啟，讓您設定屬性；例如，影像新增至資料格前的影像來源。  
  
## <a name="see-also"></a>另請參閱  
 [影像、文字方塊、矩形和線條 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/images-text-boxes-rectangles-and-lines-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
