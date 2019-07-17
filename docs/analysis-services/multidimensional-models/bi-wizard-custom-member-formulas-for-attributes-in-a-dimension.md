---
title: 在維度中設定屬性的自訂成員公式 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 29b4d83956e6963aa7df0b4a1afd11edda6c83c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68179104"
---
# <a name="bi-wizard---custom-member-formulas-for-attributes-in-a-dimension"></a>BI 精靈 - 維度中屬性的自訂成員公式
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  將自訂成員公式增強功能加入至 Cube 或維度以取代預設彙總，預設彙總與使用多維度運算式 (MDX) 運算式之結果的維度成員相關聯。 (在維度中，此增強功能會於指定的屬性上設定 **CustomRollupColumn** 屬性。)  
  
> [!NOTE]  
>  只有以現有資料來源為基礎的維度，才可以使用自訂成員公式。 針對不使用資料來源而建立的維度，您必須執行結構描述產生精靈來建立資料來源檢視後，才能加入自訂成員公式。  
  
 若要加入自訂成員公式，您可使用 [商業智慧精靈]，並於 [選擇增強功能]  頁面上選取 [建立自訂成員公式]  選項。 然後，此精靈會引導您逐步完成選取要套用自訂成員公式的維度，並啟用自訂成員公式。  
  
## <a name="selecting-a-dimension"></a>選取維度  
 在精靈的第一個 [建立自訂成員公式]  頁面上，您指定要套用自訂成員公式的維度。 加入到此選取維度的自訂成員公式增強功能，會造成維度的變更。 包含選取之維度的所有 Cube，都會繼承這些變更。  
  
## <a name="enabling-a-custom-member-formula"></a>啟用自訂成員公式  
 在第二個 [建立自訂成員公式]  頁面上，您將包含自訂成員公式的來源資料行與維度中的一個或多個屬性相關聯。 在 [屬性]  資料行中，選取您要與自訂成員公式資料行相關聯之屬性旁的核取方塊。 選取每個屬性之後，精靈會顯示 [選取資料行]  對話方塊。 在此對話方塊中，按一下包含公式之維度資料表中的資料行。 如果您要在關閉 [選取資料行]  對話方塊後變更選取項目，請按一下您要變更的 [來源資料行]  資料格，然後按一下省略符號 ([...]  ) 再次開啟 [選取資料行]  對話方塊。  
  
## <a name="see-also"></a>另請參閱  
 [使用商業智慧精靈增強維度](http://msdn.microsoft.com/library/12d995d1-75ca-4890-bf4b-a2656910b8d0)  
  
  
