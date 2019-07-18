---
title: 選取資料表和檢視 （資料摘要） (SSAS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.seltablesviewsdf.f1
ms.assetid: 6c4fafe0-e02e-47d1-b8bc-e70e872690af
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 82fcf08a84a06d33c33a520ce351f6c685092a15
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66069275"
---
# <a name="select-tables-and-views-data-feeds-ssas"></a>選取資料表和檢視表 (資料摘要) (SSAS)
  [資料表匯入精靈]  的這個頁面可讓您選取您要匯入資料的來源資料表和檢視表。 若要從 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]存取精靈，請按一下 **[模型]** 功能表上的 **[從資料來源匯入]** 。  
  
 此頁面之資料表和檢視表的外觀不保證匯入將會成功。 如果在 [模擬資訊] 頁面中指定的使用者未具備從所選資料庫讀取的權限，則匯入將會失敗。  
  
 針對使用 Windows 驗證的資料來源，目前使用者的認證會用來提取 [選取資料表和檢視表] 對話方塊中的資料表和檢視表。 至於其他資料來源，連接字串中提供的認證則用來提取資料。  
  
## <a name="uielement-list"></a>UIElement 清單  
 **資料摘要 URL**  
 顯示您選取之資料摘要的 URL。  
  
 **資料表和檢視表**  
 列出資料摘要中的資料表和檢視表。 選取您要匯入之每個資料表和檢視表旁邊的核取方塊。  
  
 **來源資料表**  
 根據資料來源的類型指定來源資料表的名稱。  
  
 **易記名稱**  
 指定來源資料表的易記名稱。 根據預設，此資料行會顯示出現在 [來源資料表]  資料行內的來源資料表名稱。  
  
 **篩選詳細資料**  
 當篩選已經套用到正在匯入的資料時，在 [篩選詳細資料]  對話方塊中顯示資料匯入篩選。 如需詳細資訊，請參閱[篩選詳細資料 &#40;SSAS&#41;](filter-details-ssas.md)。  
  
 **預覽和篩選**  
 顯示 [預覽選取的資料表]  對話方塊，此對話方塊是用來將篩選套用到匯入的資料。 如需詳細資訊，請參閱[預覽選取的資料表 &#40;SSAS&#41;](preview-selected-table-ssas.md)。  
  
 **選取相關的資料表**  
 選取與您選取之資料表和檢視表相關的資料表。  
  
  
