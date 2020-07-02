---
title: 編輯實體
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- entities [Master Data Services], changing name
ms.assetid: 6a5b9f14-6dfc-49d7-a771-e96461d4feae
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 484fdb93ac51f353de97333d115aed4591715e9a
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85813319"
---
# <a name="edit-an-entity-master-data-services"></a>編輯實體 (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  您可以在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中編輯實體。  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取 **[系統管理]** 功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱系統[管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)。  
  
### <a name="to-edit-an-entity"></a>編輯實體  
  
1.  在 [ [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]] 中，按一下 **[系統管理]**。  
  
2.  在 [**管理模型**] 頁面上，從方格中選取模型，然後按一下 [**實體**]。  
  
3.  在 [管理實體]**** 頁面的方格中，選取您要變更的實體資料列，然後按一下 [編輯]****。  
  
4.  在 [名稱]**** 方塊中，輸入實體的更新名稱。  
  
5.  在 [描述]**** 欄位中，輸入實體的更新描述。  
  
6.  在 [暫存資料表的名稱]**** 欄位中，輸入暫存資料表的更新名稱。  
  
7.  在下拉式清單中選擇 [交易記錄類型]**** 欄位的更新交易記錄類型。  
  
     如需詳細資訊，請參閱[變更實體交易記錄類型 &#40;Master Data Services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)  
  
8.  選取或取消選取 [自動建立代碼值]**** 核取方塊。  
  
     如需詳細資訊，請參閱[自動建立代碼 &#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md)。  
  
9. 選取或取消選取 [啟用資料壓縮]**** 核取方塊。 依預設會開啟資料列壓縮。  
  
     如需詳細資訊，請參閱[資料壓縮](../relational-databases/data-compression/data-compression.md)  
  
## <a name="status"></a>狀態  
 方格中的狀態資料行會顯示實體的作業狀態。 當您按一下 [儲存實體]**** 時，下列影像隨即顯示，指出正在更新實體。  
  
 ![更新狀態的圖示](../master-data-services/media/mds-statusicon-updating.png "更新狀態的圖示")  
  
 如果建立或編輯實體時發生錯誤，則會顯示下列影像。  
  
 ![錯誤狀態圖示](../master-data-services/media/mds-statusicon-error.png "錯誤狀態圖示")  
  
 如果狀態正常，則會顯示下列影像。  
  
 ![[確定] 狀態的圖示](../master-data-services/media/mds-statusicon-ok.png "[確定] 狀態的圖示")  
  
## <a name="see-also"></a>另請參閱  
 [明確階層 &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)   
 [刪除實體 &#40;Master Data Services&#41;](../master-data-services/delete-an-entity-master-data-services.md)   
 [實體 &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
  
