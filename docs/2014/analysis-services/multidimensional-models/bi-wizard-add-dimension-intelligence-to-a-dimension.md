---
title: 將維度智慧加入維度 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Business Intelligence enhancements [Analysis Services], dimension intelligence
- dimensions [Analysis Services], Business Intelligence enhancements
- dimension intelligence [Analysis Services]
- Type property
ms.assetid: b64fa386-eac2-4286-a320-0631a1887aac
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: de910ec8c845c67346c8a31b8d372efa0d3390c9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133828"
---
# <a name="add-dimension-intelligence-to-a-dimension"></a>將維度智慧加入至維度中
  將維度智慧增強功能加入至 Cube 或維度，以指定維度的標準商務類型。 此增強功能同時也會指定維度屬性的對應類型。 用戶端應用程式在分析資料時可以使用這些類型規格。  
  
 若要加入維度智慧，您可使用 [商業智慧精靈]，並於 [選擇增強功能] 頁面上選取 [定義維度智慧] 選項。 然後，此精靈會引導您逐步完成選取要套用維度智慧的維度，並為選取的維度識別屬性。  
  
## <a name="selecting-a-dimension"></a>選取維度  
 在精靈的第一個 [設定維度智慧選項] 頁面上，指定要套用維度智慧的維度。 加入到此選取維度的維度智慧增強功能，會產生維度的變更。 包含選取之維度的所有 Cube，都會繼承這些變更。  
  
> [!NOTE]  
>  如果選取 [帳戶] 作為維度，您將會指定維度的帳戶智慧。 如需詳細資訊，請參閱[將帳戶智慧加入至維度中](bi-wizard-add-account-intelligence-to-a-dimension.md)。  
  
## <a name="specifying-dimension-attributes"></a>指定維度屬性  
 在**定義維度智慧**頁面上，於**維度類型** 清單中，您所做的選取項目設定的維度`Type`屬性。 `Type`屬性設定會提供資訊給伺服器和用戶端應用程式內容的相關的維度。 部份設定只為用戶端應用程式提供指導；這些設定是選擇性的。 其他設定 (例如帳戶或時間) 決定特定的行為，並可能對實作特殊商業智慧增強功能是必要的。 例如，SQL Server Management Studio 使用維度類型來識別貨幣維度，以及設定適當的貨幣轉換規則。 [維度類型] 的預設值為 [一般]，不會對維度內容做任何假設。  
  
 選取維度類型之後，在 [維度屬性] 的 [包含] 資料行中，針對在維度中有對應屬性的每個標準屬性類型，選取其旁邊的核取方塊。 最後，在 [維度屬性] 資料行中展開下拉式清單，並在對應到所選取屬性類型的維度中選取屬性。 從清單中選取屬性，會針對屬性設定屬性 `Type` 屬性。  
  
 例如，您要將維度智慧加入至帳戶維度。 在 [維度屬性] 中，選取 [帳戶]。 然後，如果維度有 [帳戶類型] 和 [帳戶描述] 屬性，請在 [包含] 資料行中，選取 [帳戶名稱] 和 [帳戶類型] 帳戶類型的核取方塊。 在 [維度屬性] 資料行中，將這些帳戶類型分別與維度內的 [帳戶描述] 和 [帳戶類型] 屬性產生關聯。  
  
## <a name="see-also"></a>另請參閱  
 [使用商業智慧精靈定義時間智慧計算](define-time-intelligence-calculations-using-the-business-intelligence-wizard.md)  
  
  