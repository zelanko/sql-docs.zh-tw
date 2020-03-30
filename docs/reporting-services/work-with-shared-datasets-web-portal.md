---
title: 使用共用資料集 (Web 入口網站) | Microsoft Docs
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 2641ea84-9343-4e6f-aec1-25339031b163
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e034b911ec5817ac82214466fdc2bf7087e8865a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "68222765"
---
# <a name="work-with-shared-datasets---web-portal"></a>使用共用資料集 - Web 入口網站

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

您可以使用共用資料集，從報表及其他使用該資料集的目錄項目，個別管理資料集的設定。 共用資料集可以隨 KPI 搭配分頁和行動報表使用。

您可以檢視和管理入口網站內共用資料集的屬性。 入口網站可以啟動「報表產生器」來建立或編輯共用資料集。

## <a name="create-a-shared-dataset"></a>建立共用資料集
  
您可以執行以下步驟來建立新的共用資料集。  
  
1.  從功能表列選取 [新增]。  
  
2.  選取 [資料集]  。  
  
    ![ssRSDataset-NewDataset](../reporting-services/media/ssrsdataset-newdataset.png)  
  
3.  將會啟動 [報表產生器]，或提示您下載它。  
  
4.  在 [新報表或資料集]  對話方塊，選取針對此資料集要使用的資料來源連線。 您可能需要瀏覽到共用資料來源的位置。  
  
5.  選取 [建立]  。  
  
6.  建置您的資料集，然後選取左上方的 [儲存]  圖示來將資料集儲存回報表伺服器。  
  
## <a name="manage-an-existing-shared-dataset"></a>管理現有的共用資料集
  
您可以執行以下步驟來管理現有的共用資料集。  
  
> [!NOTE]
> 如果您在資料夾中沒有看到共用資料集，請確定您正在檢視資料集。 您可以從入口網站右上角的功能表列選取 [檢視]  。 請確定已選取 [資料集]  。  
  
1.  針對您要管理的資料庫選取**省略符號 (...)** 。  
  
    ![ssRSDataset-Ellipse](../reporting-services/media/ssrsdataset-ellipse.png)  
  
2.  選取 [管理]  會開啟編輯畫面。  
  
    ![ssRSDataset-Manage](../reporting-services/media/ssrsdataset-manage.png)  
  
## <a name="properties"></a>屬性
  
在 [屬性] 畫面中，您可以變更該資料集的 [名稱]  和 [描述]  。 您也可以 [刪除]  、[移動]  、[在報表產生器中編輯]  、[下載]  或 [取代]  。  
  
![ssRSdataset-Properties](../reporting-services/media/ssrsdataset-properties.png)  
  
## <a name="caching"></a>Caching
  
您有幾個選項可以快取資料集的資料。 先從簡單的選取步驟開始。  
  
1.  [永遠以最新的資料執行此報表]  會在要求時針對資料來源進行查詢。  
  
2.  [快取此報表的複本並在可用時加以使用]  會將資料的暫存複本置於快取中，以供使用此資料集的項目使用。 快取通常會改善效能，因為資料是從快取傳回，而非再次執行資料集查詢。  
  
![ssRSDataset-Caching1](../reporting-services/media/ssrsdataset-caching1.png)  
  
選取 [快取此報表的複本並在可用時加以使用]  會顯示更多選項。  
  
![ssRSDataset-Caching2](../reporting-services/media/ssrsdataset-caching2.png)  
  
### <a name="cache-expiration"></a>快取到期  
  
您可以控制是否要讓共用資料集的快取在一段時間後到期，您也可以選擇用排程來控制。 您可以使用共用排程。  
  
![ssRSDataset-Caching3](../reporting-services/media/ssrsdataset-caching3.png)  
  
> [!NOTE]
> 設定到期時間不會重新整理快取。 若沒有快取重新整理計劃，則會在資料集下次執行的時候重新整理資料。  
  
### <a name="cache-refresh-plans"></a>快取重新整理計劃  
  
您可以使用「快取重新整理計劃」來建立排程，以供預先載入含共用資料集之資料暫存複本的快取。 重新整理計劃包括排程和選項，可指定或覆寫參數的值。 您不能覆寫標示為唯讀的參數值。 您可以建立並使用多個重新整理計劃。   
  
可讓您加入、刪除、變更快取重新整理計劃之共用資料集的預設角色指派有：[內容管理員]、[我的報表] 和 [發行者]。  
  
套用上述的快取選項之後，您可以接著定義快取重新整理計劃。 若要這麼做，請在套用快取設定之後，選取顯示的 [管理重新整理計劃]  連結。 隨即會顯示 [快取重新整理計劃] 頁面。   
  
若要建立新的快取重新整理計劃，選取 [新增快取重新整理計劃]  。 接下來，您可以輸入計劃的名稱並指定排程。 如果資料集已定義參數，則您可以看到它們列出且可為其提供值，除非它們被標示為唯讀。  
  
當您完成之後，即可選取 [建立快取重新整理計劃]  。  
  
![ssRSDataset-Caching4](../reporting-services/media/ssrsdataset-caching4.png)  
  
> [!NOTE]
> 必須正在執行 SQL Server Agent 才能建立快取重新整理計劃。  
  
您接著可以 [編輯]  或 [刪除]  列出的計劃。 當只有選取一個快取重新整理計劃時，才會啟用 [從現有的新增]  選項。 這個選項會建立從原始計劃複製的新重新整理計劃。 [快取重新整理計劃] 頁面開啟時會預先填入所選取計劃的詳細資料。 接著，您就可以修改重新整理計劃選項，然後使用新的描述儲存該計劃。  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
