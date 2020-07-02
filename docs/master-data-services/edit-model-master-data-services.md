---
title: 編輯模型
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], changing name
ms.assetid: 399eed32-7c61-4239-9c06-996a65219518
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 2a0a2bd63e5b69cd9e0b206f18414b41c823441d
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85812988"
---
# <a name="edit-model-master-data-services"></a>編輯模型 (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，您可以變更模型的名稱和描述，並指定您要保留交易記錄的天數。  
  
 如需詳細資訊，請參閱[交易 &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)。  
  
### <a name="to-change-a-model"></a>變更模型  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 **[模型檢視]** 頁面上，從功能表列指向 **[管理]** ，然後按一下 **[模型]**。  
  
3.  從 [管理模型] **** 頁面的方格中，選取您要變更名稱或描述之模型的資料列。  
  
4.  按一下 **[編輯]** 。  
  
5.  在 [名稱] **** 方塊中，輸入模型的更新名稱。  
  
6.  在 [描述] **** 欄位中，輸入模型的更新描述。  
  
7.  在 [Log Retention Days] (記錄保留天數) **** 欄位中，選取其中一個選項來保留記錄資料。 預設值為 [系統設定] ****，表示會從 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中的系統設定繼承值。 如需詳細資訊，請參閱 [系統設定 &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md)。  
  
     若要覆寫系統設定而不移除交易記錄資料，請選取 [否] ****。 若只要保留今天的記錄資料並截斷過去幾天的記錄資料，請選取 **[是]** ，然後將 [**天數**] 欄位設為0。 若要保留指定天數的記錄資料，請選取 [是] **** ，然後將 [天數] **** 欄位設為該天數。  
  
8.  按一下 **[儲存模型]**。  
  
 方格中的 [狀態] **** 資料行會顯示模型上的作業狀態。 當您按一下 [**儲存模型**] 按鈕時，會顯示![更新](../master-data-services/media/mds-model-status-updating.png "更新")影像，表示正在更新模型。 如果建立或編輯模型時發生錯誤，則會顯示![錯誤](../master-data-services/media/mds-model-status-error.png "錯誤")影像。 否則，狀態會是 [確定]，而且會顯示 [![確定]](../master-data-services/media/mds-model-status-ok.png "[確定]")影像。  
  
## <a name="see-also"></a>另請參閱  
 [建立模型 &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)   
 [刪除模型 &#40;Master Data Services&#41;](../master-data-services/delete-a-model-master-data-services.md)   
 [模型 &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)  
  
  
