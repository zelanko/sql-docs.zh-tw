---
title: 建立訂閱檢視以匯出資料
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- subscription views [Master Data Services], creating
- creating subscription views [Master Data Services]
ms.assetid: a5e28961-af16-414a-9845-d2e06aac5214
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 524ff4934adf2317daceff64f70ce4ae0afb7424
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73728476"
---
# <a name="create-a-subscription-view-to-export-data-master-data-services"></a>建立訂閱檢視以匯出資料 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  建立訂閱檢視，以將 Master Data Services 資料匯出至訂閱系統。 您正要建立 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫中資料的檢視。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[整合管理]** 功能區域的權限。 如需詳細資訊，請參閱[功能區域許可權 &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱 [管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)，您就可以在群組中加入及移除使用者。  
  
### <a name="to-create-and-edit-a-subscription-view"></a>建立和編輯訂閱檢視  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，按一下 **[整合管理]**。  
  
2.  按一下功能表列上的 **[建立檢視表]**。  
  
3.  在 [訂閱檢視] **** 頁面上，按一下 [加入] **** 建立檢視，或按一下 [編輯] **** 編輯檢視。 隨即會在右側顯示面板。  
  
4.  在 [建立訂閱檢視] **** 窗格的 [名稱] **** 方塊中，輸入該檢視的名稱。  
  
     在 [編輯訂閱檢視] **** 窗格的 [名稱] **** 方塊中，輸入該檢視的已更新名稱。  
  
5.  從 **[模型]** 清單中選取模型。  
  
6.  選取 [Include soft-deleted members]\ (包含虛刪除成員) **** 以包含檢視中的虛刪除成員。  
  
7.  在 [版本選項] **** 中選取 [版本] **** 或 [版本旗標] ****，然後從對應的清單中選取。  
  
    > [!TIP]  
    >  根據版本旗標建立訂閱檢視。 當您鎖定版本時，您可以重新指派旗標給開啟的版本，而不用更新訂閱檢視。  
  
8.  選取 [資料來源] **** 選項中的 [實體] **** 或 [衍生階層] **** ，然後從對應的清單中選取。  
  
9. 從 **[格式]** 清單中選取訂閱檢視格式。  
  
10. 如果您從 **[格式]** 清單中選擇 **[明確層級]** 或 **[衍生層級]** ，請輸入階層內要加入檢視中的層級數。  
  
11. 按一下 [檔案]  。  
  
## <a name="view-information"></a>檢視資訊  
 對於每個建立的檢視，會將含十個資料行的資料列加入方格中。 下表描述該資料行。  
  
|資料行|描述|  
|------------|-----------------|  
|狀態|檢視狀態。<br /><br /> 當您按一下 [**儲存**] 時，會顯示 [![正在更新狀態](../master-data-services/media/mds-statusicon-updating.png "更新狀態的圖示")影像] 圖示，表示正在更新此視圖。<br /><br /> 如果建立或編輯檢視時發生錯誤，則會顯示 [![錯誤狀態](../master-data-services/media/mds-statusicon-error.png "錯誤狀態圖示")影像] 圖示。<br /><br /> 否則，狀態為 [確定]，並顯示 [![確定狀態影像] 圖示](../master-data-services/media/mds-statusicon-ok.png "[確定] 狀態的圖示")。|  
|名稱|訂閱檢視名稱。|  
|模型|模型名稱。|  
|版本|版本名稱。|  
|版本旗標|版本旗標名稱。|  
|衍生階層|衍生階層名稱。|  
|實體|實體名稱。|  
|[格式]|指定檢視中資料的類型。|  
|層級|指定檢視中的層級數目 (僅用於明確層級或衍生層級檢視格式)。|  
|包含刪除成員|表示檢視中是否包含虛刪除成員。|  
  
 當您按一下檢視時，會顯示下列資訊。  
  
-   **建立者**：建立視圖的使用者名稱。  
  
-   **于**：建立視圖的日期和時間。  
  
-   **更新者**：上次更新視圖的使用者名稱。  
  
-   **于**：上次更新視圖的日期和時間。  
  
## <a name="see-also"></a>另請參閱  
 [總覽：匯出資料 &#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md)   
 [刪除訂閱視圖 &#40;Master Data Services&#41;](../master-data-services/delete-a-subscription-view-master-data-services.md)   
 [建立 &#40;Master Data Services 的版本旗標&#41;](../master-data-services/create-a-version-flag-master-data-services.md)  
  
  
