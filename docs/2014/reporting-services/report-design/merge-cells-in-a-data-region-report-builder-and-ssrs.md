---
title: 在資料區中合併資料格 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 43551300-89b2-4f4e-af09-69084324afaf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 97e9280512b75aebfccb93c0e11e5402136fa6f8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105570"
---
# <a name="merge-cells-in-a-data-region-report-builder-and-ssrs"></a>在資料區中合併資料格 (報表產生器及 SSRS)
  您可以在資料區域中合併資料格來結合資料格、增進資料區域外觀，或為資料行群組與資料列群組提供橫跨的標籤。  
  
> [!NOTE]  
>  資料格僅能在資料區域的每個區域內進行合併：邊角、資料行標頭、群組定義 (或資料列標頭) 以及主體。 您無法合併跨越區域界限的資料格。 例如，您無法將資料區邊角區域中的資料格與資料列群組區域中的資料格合併。 如需 tablix 區域的詳細資訊，請參閱[&#40;報表產生器和 SSRS&#41;清單](tables-matrices-and-lists-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-merge-cells-in-a-data-region"></a>若要在資料區中合併資料格  
  
1.  在報表設計介面的資料區中，按一下要合併的第一個資料格。 按住滑鼠左鍵，以垂直或水平方向拖曳來選取相鄰的資料格。 選取的資料格就會反白顯示。  
  
2.  以滑鼠右鍵按一下選取的資料格，然後選取 [合併資料格]  。 選取的資料格就會結合到單一的資料格中。  
  
3.  重複步驟 1 和 2，在資料區域中合併其他相鄰的資料格。  
  
## <a name="see-also"></a>另請參閱  
 [Tablix 資料區 &#40;報表產生器及 SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [資料表 &#40;報表產生器及 SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [矩陣 &#40;報表產生器及 SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [清單 &#40;報表產生器及 SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [清單 &#40;報表產生器及 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
