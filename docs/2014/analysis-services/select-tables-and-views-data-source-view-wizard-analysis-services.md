---
title: 選取資料表和檢視 （資料來源檢視精靈） (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.datasourceviewwizard.selecttablesandviews.f1
ms.assetid: ea7d1232-f213-46e9-90d9-0fd616ca003d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f18e9c5817de5e98ae21726b235d60d8d31e7d66
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104008"
---
# <a name="select-tables-and-views-data-source-view-wizard-analysis-services"></a>選取資料表和檢視 (資料來源檢視精靈) (Analysis Services)
  使用 [選取資料表和檢視] 頁面，從您想要包含在資料來源檢視裡的資料來源中，選取資料表或檢視。  
  
## <a name="options"></a>選項。  
 **可用的物件**  
 列出資料來源結構描述中的資料表和檢視。 如果列出了一項以上的結構描述，每個物件的名稱都會以結構描述名稱為前置詞。 如果只列出一項結構描述，物件名稱就不會有結構描述的名稱作為前置詞。  
  
 若要以遞增或遞減的順序重新排列清單，請按一下 [名稱] 或 [類型]。  
  
 **包含的物件**  
 列出要包含在資料來源檢視中的資料表和檢視。  
  
 若要以遞增或遞減的順序重新排列清單，請按一下 [名稱] 或 [類型]。  
  
 **篩選**  
 篩選 [可用的物件] 之下所列的物件。 鍵入字串，然後按一下 [篩選] 即可只列出包含指定字串的名稱。 若要尋找完全相同的字元字串，請將字串置於雙引號之間。 篩選不區分大小寫。  
  
 您可以將下表所列的萬用字元，包含在篩選字串中的任何地方。  
  
|萬用字元|值|  
|------------------------|-----------|  
|**\***|任何字元字串。|  
|**%**|任何字元字串。|  
|**?**|單一字元。|  
|**「** 字串 **」**|字元組成的常值字串 此萬用字元會符合物件名稱裡的任何子字串。|  
  
 **顯示系統物件**  
 顯示 [可用的物件] 之下的系統物件。 唯有在資料來源提供者公開了系統物件之後，才可以使用此選項。 從 [包含的物件] 清單中移除系統物件，就會自動選取此選項。  
  
 **加入相關的資料表**  
 加入與 [包含的物件] 之下所列物件相關的所有資料表。 此選項不會加入檢視。 但是，此選項會加入已分割的資料表。 如果在精靈的 [名稱比對] 頁面上選取了名稱比對準則，此選項還會依據您選取的準則，來包含邏輯上相關的資料表。 如果資料表與新加入的相關資料表相關聯，且如果其具有與原來資料表相同的結構，則也會包含這些資料表。  
  
## <a name="see-also"></a>另請參閱  
 [資料來源檢視精靈 F1 說明&#40;Analysis Services&#41;](data-source-view-wizard-f1-help-analysis-services.md)   
 [多維度模型中的資料來源檢視](multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
