---
title: 內嵌和共用資料集 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: adc95cc0-d15a-413d-bc5a-302eab37a069
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 069c8900d5d9939567dd5e59f2f5f6547b0044af
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041709"
---
# <a name="embedded-and-shared-datasets-report-builder-and-ssrs"></a>內嵌和共用資料集 (報表產生器及 SSRS)
  在報表中，資料集代表在外部資料來源上執行查詢時所傳回的報表資料。 資料集取決於包含外部資料來源之相關資訊的資料連接。 資料本身不會包含在報表定義中。 資料集包含查詢命令、欄位集合、參數、篩選，以及包含區分大小寫和定序的資料選項。 資料集有以下兩種不同的類型：  
  
-   **共用資料集。** 共用資料集是在報表伺服器上發行，可供多個報表使用。 共用資料集必須以共用資料來源為基礎。 共用資料集可透過建立快取重新整理計劃的方式快取和排程。  
  
-   **內嵌資料集。** 內嵌資料集是在單一報表中定義，只供單一報表使用。  
  
 這兩種資料集之間的差異在於建立、儲存和管理的方式。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="shared-datasets"></a>共用資料集  
 您可以使用共用資料集來提供多個報表能夠使用的查詢。 共用資料集會儲存在報表伺服器上，並且與報表或共用資料來源分開管理。 例如，報表伺服器管理員可能會更新查詢以利用改善的索引或其他最佳化查詢效能的方法。  
  
 建議您盡量使用共用資料集。 您可以最佳化查詢或快取查詢結果，以獲得更佳的報表效能。 共用資料集可讓資料存取的管理更輕鬆，並且有助於提升報表和報表所存取資料集的安全性，以及提高效能。  
  
 在報表設計師中，您可以建立共用資料集做為報表專案的一部分，以及控制是否要將它們部署至報表伺服器。 但是，您無法瀏覽至報表伺服器，然後選取要加入至報表的共用資料集。  
  
 在報表產生器中，您可以執行下列作業：  
  
1.  若要建立共用資料集，請使用共用資料集設計檢視。 您可以將它儲存至報表伺服器或 SharePoint 網站，以便與其他報表共用。 您也可以瀏覽至報表伺服器，然後編輯現有的共用資料集。 在此檢視中，您可以建立查詢並設定所有資料集選項。 如需詳細資訊，請參閱[共用資料集設計檢視 &#40;報表產生器&#41;](../report-builder/shared-dataset-design-view-report-builder.md)。  
  
2.  若要將共用資料集加入至報表，請在 [報表設計檢視] 中開啟報表產生器。 從精靈或 [報表資料] 窗格中，瀏覽到報表伺服器，並選取您要加入至報表的共用資料集。 在此檢視中，除非加入欄位，否則您無法變更查詢。 您可以覆寫其他資料選項和加入篩選。 不過不能移除篩選。  
  
3.  下表比較可在報表伺服器上針對共用資料集的定義設定的屬性，以及針對報表定義中共用資料集的執行個體設定的屬性。  
  
    |屬性|定義的設定注意事項|執行個體的設定注意事項|  
    |--------------|--------------------------------------------|------------------------------------------|  
    |查詢文字|設定查詢，包括將它定義為運算式。|無法變更查詢。|  
    |查詢參數|無法參考報表參數<br /><br /> 包含預設值<br /><br /> 包含唯讀旗標|設定未在定義中標記為唯讀的參數|  
    |篩選|定義篩選|無法檢視或變更屬於定義之一部分的資料集篩選<br /><br /> 可以建立其他篩選|  
    |資料來源|必須為共用資料來源|無法變更資料來源|  
    |欄位|來自查詢命令的欄位<br /><br /> 導出欄位不屬於資料集定義的一部分|檢視欄位，但是無法變更欄位<br /><br /> 根據您將共用資料集加入至報表時的查詢，欄位集合是靜態的。 若要更新，請按一下 **[資料集屬性]** 對話方塊中的 **[重新整理欄位]** 。 實際的欄位集合是定義中目前的查詢所傳回的任何內容。<br /><br /> 加入導出欄位|  
    |資料集|資料選項，例如區分大小寫|覆寫執行個體中的資料選項|  
  
## <a name="embedded-datasets"></a>內嵌資料集  
 如果您要從外部資料來源取得資料，並且僅用於一個報表中，則使用內嵌資料集。 當您想要建立的查詢沒有其他相依性而且不需要用於多個報表時，內嵌資料集將會很實用。  
  
 若要建立或編輯內嵌資料集，請使用 [報表資料] 窗格。 建立資料集之後，您可以在 **[資料集屬性]** 對話方塊中設定屬性。  
  
## <a name="see-also"></a>另請參閱  
 [內嵌和共用資料連接或資料來源 &#40;報表產生器及 SSRS&#41;](../embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [建立共用資料集或內嵌資料集 &#40;報表產生器及 SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [將資料加入至報表&#40;報表產生器及 SSRS&#41;](report-datasets-ssrs.md)   
 [資料集欄位集合 &#40;報表產生器及 SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)   
 [報表產生器中的資料連接、資料來源及連接字串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)   
 [報表產生器中的資料連接、資料來源及連接字串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)  
  
  
