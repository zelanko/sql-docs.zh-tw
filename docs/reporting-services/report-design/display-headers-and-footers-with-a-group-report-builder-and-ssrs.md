---
title: 與群組一起顯示頁首和頁尾 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8eb7d648-4df2-491a-96cb-99e55629d617
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3068cf6494dfc790f2990f8e872dd9365e3594f5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33021015"
---
# <a name="display-headers-and-footers-with-a-group-report-builder-and-ssrs"></a>與群組一起顯示頁首和頁尾 (報表產生器及 SSRS)
  您可以協助控制靜態資料列 (例如群組頁首或頁尾) 是否會與動態資料列 (與 Tablix 資料區中的群組有關聯) 一起轉譯。  
  
 若要在多個頁面上重複所有資料行標題或資料列標題，您可以設定 Tablix 資料區的屬性。 如需詳細資訊，請參閱[在多個頁面上顯示資料列和資料行標頭 (報表產生器及 SSRS)](display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)。  
  
 若要控制與巢狀群組相關聯之動態資料列和資料行的轉譯行為，或與標籤或小計相關聯之靜態資料列和資料行的轉譯行為，您必須設定 Tablix 成員的屬性。 Tablix 成員代表靜態或動態資料列或資料行。 靜態成員會重複一次。 例如，總計資料列就是靜態資料列。 動態成員會針對每個群組執行個體重複一次。 例如，與具有群組運算式 [Territory] 之群組相關聯的資料列會針對領域的每個唯一值重複一次。 如需 Tablix 成員的詳細資訊，請參閱 [Tablix 資料區資料格、資料列及資料行 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。  
  
 您可以在 [群組] 窗格中選取 Tablix 成員，然後在 [屬性] 窗格中設定 **[KeepWithGroup]**、 **[KeepTogether]** 和 **[RepeatOnNewPage]** 屬性。 使用 **[KeepWithGroup]** 可在與群組相同的頁面上顯示群組頁首和頁尾。 使用 **[KeepTogether]** 可以與某個群組的資料列或資料行一併顯示靜態成員。 使用 **[RepeatOnNewPage]** 可在至少顯示一個 **[KeepWithGroup]** 值所指定的完整資料列群組成員執行個體的每一頁上，重複群組頁首或頁尾。 資料行群組成員不支援 **[RepeatOnNewPage]** 。  
  
> [!NOTE]  
>  **KeepWithGroup**、**KeepTogether** 和 **RepeatOnNewPage** 是群組成員屬性，可以使用 [群組] 窗格的 [進階模式] 設定。 如需詳細資訊，請參閱[群組窗格 &#40;報表產生器&#41;](../../reporting-services/report-design/grouping-pane-report-builder.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-keep-a-static-row-with-a-set-of-dynamic-rows-associated-with-a-row-group"></a>若要將靜態資料列和一組與資料列群組相關聯的動態資料列保持在一起  
  
1.  在設計介面上，按一下 Tablix 資料區中的任意位置來選取它。 [群組] 窗格會顯示資料區的資料列群組和資料行群組。  
  
2.  在 [群組] 窗格的右邊按一下向下箭頭，然後按一下 **[進階模式]**。 [資料列群組] 窗格會顯示資料列群組階層的階層式靜態和動態成員。  
  
3.  按一下對應至要與群組資料列保持在一起的資料列標頭或頁尾的靜態成員。 [屬性] 窗格會顯示 **[Tablix 成員]** 屬性。  
  
4.  在 [屬性] 窗格中，按一下 [KeepWithGroup]，然後從下拉式清單選擇下列其中一個值：  
  
    -   **無** ：選取這個選項可指出沒有將此成員與所選取資料列群組的成員保持在一起的喜好設定。  
  
    -   **之前** ：選取這個選項可將此成員與先前群組的成員保持在一起。 您可以將此選項用於群組頁尾資料列。  
  
    -   **之後** ：選取這個選項可將此成員與後續群組的成員保持在一起。 您可以將此選項用於群組頁首資料列。  
  
5.  (選擇性) 預覽報表。 在可能的狀況下，報表轉譯器都會將此成員與指定的資料列群組成員保持在一起。  
  
### <a name="to-keep-a-static-column-with-a-set-of-dynamic-columns-associated-with-a-column-group"></a>若要將靜態資料行和一組與資料行群組相關聯的動態資料行保持在一起  
  
1.  在設計介面上，按一下 Tablix 資料區中的任意位置來選取它。 [群組] 窗格會顯示資料區的資料列群組和資料行群組。  
  
2.  在 [群組] 窗格的右邊按一下向下箭頭，然後按一下 **[進階模式]**。 [資料行群組] 窗格會顯示資料行群組階層的階層式靜態和動態成員。  
  
3.  按一下對應至要與群組資料行保持在一起的靜態資料行的靜態成員。 [屬性] 窗格會顯示 **[Tablix 成員]** 屬性。  
  
4.  在 [屬性] 窗格中，按一下 [KeepWithGroup]，然後從下拉式清單選擇下列其中一個值：  
  
    -   **無** ：選取這個選項可指出沒有將此成員與所選取資料行群組的成員保持在一起的喜好設定。  
  
    -   **之前** ：選取這個選項可將此成員與先前群組的成員保持在一起。 您可能將此選項用於顯示在所指定資料行群組成員之前的資料行標籤。  
  
    -   **之後** ：選取這個選項可將此成員與後續群組的成員保持在一起。 您可能將此選項用於顯示在所指定資料行群組成員之後的資料行總計。  
  
5.  (選擇性) 預覽報表。 在可能的狀況下，報表轉譯器都會將此成員與指定的資料行群組成員保持在一起。  
  
## <a name="see-also"></a>另請參閱  
 [Tablix 資料區資料格、資料列及資料行 (報表產生器及 SSRS)](tablix-data-region-report-builder-and-ssrs.md)   
 
  
  
