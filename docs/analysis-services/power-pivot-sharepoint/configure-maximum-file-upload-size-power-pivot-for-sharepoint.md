---
title: "設定檔案上傳大小上限 (Power Pivot for SharePoint) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ac516c63-1e79-4ae8-bca6-32d3c1a09c00
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6e79739162ee4eba9fde6af1efddd7b5b273b73d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="configure-maximum-file-upload-size-power-pivot-for-sharepoint"></a>設定檔案上傳的大小上限 (Power Pivot for SharePoint)
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿經常包含大量的資料，這些資料產生的檔案會超出 SharePoint 上傳所允許的檔案大小上限。 當您嘗試上傳的檔案超出上限時，您將會得到以下 SharePoint 錯誤：  
  
-   「指定的檔案超過支援的檔案大小上限。」  
  
 若要提高檔案大小，一開始請將 Excel Services 的 [最大活頁簿大小] 調整為 50 MB。 這樣會將 Excel 的檔案大小上限對齊 SharePoint Web 應用程式的檔案大小上限 (SharePoint 2010 中的預設值為 50 MB，SharePoint 2013 中的預設值為 200 MB)。 如果您的檔案大小超出 50 MB，請同時針對 Excel Services 和 Web 應用程式增加檔案大小限制。  
  
 您必須是 SharePoint 管理員，才能變更檔案上傳大小上限。  
  
### <a name="configure-maximum-file-size-for-excel-services"></a>設定 Excel Services 的檔案大小上限  
  
1.  在 [管理中心] 的 [應用程式管理] 中，按一下 **[管理服務應用程式]**。  
  
2.  按一下 Excel Services 應用程式的名稱。  
  
3.  按一下 [信任的檔案位置]。  
  
4.  按一下此位置來編輯屬性。 根據預設，Excel Services 會將預設 Web 應用程式視為信任的網站。 如果您要使用預設 Web 應用程式，請按一下 [http://] 開啟這個位置的組態頁面。  
  
5.  捲動到 [活頁簿內容]。  
  
6.  在 [最大活頁簿大小] 中，將檔案大小從 10 (預設值) 增加到 50 或是可容納您所使用之檔案的較大的大小。  
  
     根據預設，50 MB 是 SharePoint Web 應用程式的檔案上傳大小上限。 如果您將 [最大活頁簿大小] 設定為大於 50 MB 的數字，請遵循下一個程序的步驟，將 SharePoint Web 應用程式的 [最大上傳大小] 增加為相同的值。  
  
     您可以指定的最大值是 2 GB (或是管理中心內指定的 2047 MB)。  
  
7.  按一下 **[確定]**。  
  
### <a name="configure-maximum-file-size-for-a-sharepoint-web-application"></a>設定 SharePoint Web 應用程式的檔案大小上限  
  
1.  在管理中心的 [應用程式管理] 中，按一下 **[管理 Web 應用程式]**。  
  
    > [!NOTE]  
    >  只有當您在 Excel Services 中增加 [最大活頁簿大小] 時，才執行以下步驟。  
  
2.  選取應用程式 (例如 **SharePoint - 80**)。  
  
3.  在 Web 應用程式功能區中，按一下 [一般設定] 按鈕上的向下箭頭。  
  
4.  按一下 [一般設定]。  
  
5.  捲動到 [最大上傳大小]。  
  
6.  將此屬性設定為與 Excel Services 中 [最大活頁簿大小] 相同或更大的數字。  
  
7.  按一下 **[確定]**。  
  
  

