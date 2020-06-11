---
title: 選取資料表和視圖（SSAS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.seltablesviews.f1
ms.assetid: 5e8121cc-03f0-4168-98cf-63c5c032bb0b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cf29721888fb672c242baa8a5984da4de40cd020
ms.sourcegitcommit: 18a7c77be31f9af92ad9d0d3ac5eecebe8eec959
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/26/2020
ms.locfileid: "83858134"
---
# <a name="select-tables-and-views-ssas"></a>選取資料表和檢視表 (SSAS)
  [資料表匯入精靈]**** 的這個頁面可讓您選取您要匯入資料的來源資料表和檢視表。 若要從 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]存取精靈，請按一下 **[模型]** 功能表上的 **[從資料來源匯入]**。  
  
 此頁面之資料表和檢視表的外觀不保證匯入將會成功。 如果在 [模擬資訊] 頁面中指定的使用者未具備從所選資料庫讀取的權限，則匯入將會失敗。  
  
 針對使用 Windows 驗證的資料來源，目前使用者的認證會用來提取 [選取資料表和檢視表] 對話方塊中的資料表和檢視表。 至於其他資料來源，連接字串中提供的認證則用來提取資料。  
  
## <a name="ui-element-list"></a>UI 元素清單  
 **Server**  
 顯示您已連接的伺服器。  
  
 **Database**  
 顯示您已選取的資料庫。  
  
 **資料表和檢視表**  
 列出資料庫中的資料表和檢視表。 選取您要匯入之每個資料表和檢視表旁邊的核取方塊。  
  
 **來源資料表**  
 根據資料來源的類型指定來源資料表的名稱。  
  
 **結構描述**  
 指定其中包含來源資料表的結構描述。 視資料庫的類型而定，結構描述具有做為其他物件 (例如資料表) 之容器的作用，而且也表示這些物件的擁有權。  
  
 **易記名稱**  
 指定來源資料表的易記名稱。 根據預設，此資料行會顯示出現在 [來源資料表]**** 資料行內的來源資料表名稱。 如果您要使用不同於來源資料庫中使用的名稱，請變更這個名稱。  
  
 **篩選詳細資料**  
 當篩選已經套用到正在匯入的資料時，在 [篩選詳細資料]**** 對話方塊中顯示資料匯入篩選。 如需詳細資訊，請參閱[篩選詳細資料 &#40;SSAS&#41;](filter-details-ssas.md)。  
  
 **預覽和篩選**  
 顯示 [預覽選取的資料表]**** 對話方塊，此對話方塊是用來將篩選套用到匯入的資料。 如需詳細資訊，請參閱[預覽選取的資料表 &#40;SSAS&#41;](preview-selected-table-ssas.md)。  
  
 **選取相關資料表**  
 選取以匯入與已選取之資料表和檢視表相關的資料表和檢視表。  
  
  
