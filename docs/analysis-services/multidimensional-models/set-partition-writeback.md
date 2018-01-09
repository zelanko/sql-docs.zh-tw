---
title: "設定分割區回寫 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- write-enabled partitions [Analysis Services]
- partitions [Analysis Services], writeback
- partitions [Analysis Services], write-enabled
- writeback [Analysis Services], partitions
ms.assetid: 38bb09cc-2652-4971-8373-0cf468cdc7a6
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c1e6971bd8c1bc228386ad5b39a498f0e0ed5d42
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="set-partition-writeback"></a>設定分割區回寫
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]如果您啟用寫入的量值群組，使用者可以變更 cube 資料，在瀏覽，稱為回寫資料表，不在 cube 資料或來源資料的個別資料表中儲存的變更時。 瀏覽可寫入分割區的使用者，會看到所有變更在分割區的回寫資料表中產生的結果。  
  
 您可以瀏覽或刪除回寫資料。 您也可以將回寫資料轉換為分割區。 在可寫入分割區上，您可以使用 Cube 角色來授與讀取/寫入存取權給使用者和使用者群組，並限制對分割區中的特定資料格或資料格群組的存取。  
  
 如需有關回寫的簡短影片簡介，請參閱＜ [Analysis Services 的 Excel 2010 回寫](http://go.microsoft.com/fwlink/p/?LinkId=394951)＞。 如需此功能的更詳細說明，請參閱部落格文章系列： [Building a Writeback Application with Analysis Services](http://go.microsoft.com/fwlink/?LinkId=394977)(使用 Analysis Services 建立回寫應用程式) (部落格文章)。  
  
> [!NOTE]  
>  只有 SQL Server 關聯式資料庫和資料超市才支援回寫，且回寫僅適用於 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多維度模型。  
  
## <a name="how-to-write-enable-a-partition"></a>如何啟用分割區的寫入功能  
 您可以在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的 Cube 設計師中啟用分割區本身的寫入功能，來啟用分割區之量值群組的寫入功能。  
  
-   在 Cube 設計師的 [資料分割] 索引標籤中，以滑鼠右鍵按一下資料分割並選擇 [回寫設定]。  
  
-   在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，展開資料庫 | Cube | 量值群組，然後以滑鼠右鍵按一下 [回寫] 並選擇 [啟用回寫]。  
  
 只有使用 SUM 彙總的量值才支援回寫。 在 AdventureWorks 範例資料庫，您可以使用「銷售目標」量值群組測試回寫行為。  
  
 啟用分割區的寫入功能時，您需要指定儲存回寫資料表的資料表名稱和資料來源。 此資料表會記錄量值群組後續的任何變更。  
  
## <a name="browse-writeback-data-in-a-partition"></a>瀏覽分割區中的回寫資料  
 您可以在 [瀏覽資料] 對話方塊中瀏覽 Cube 的回寫資料表內容，在 Cube 設計師的 [資料分割] 索引標籤上，以滑鼠右鍵按一下可寫入的資料分割，即可存取此對話方塊。  
  
## <a name="delete-writeback-data-or-disable-writeback"></a>刪除回寫資料或停用回寫  
 刪除回寫資料會清除回寫快取；在刪除該資料之後，隨即會重新開始執行其他回寫工作。 停用 Cube 分割區的回寫會直接關閉該資料分割的回寫功能。  
  
## <a name="convert-writeback-data-to-a-partition"></a>將回寫資料轉換為分割區  
 您可以將分割區之回寫資料表中的資料轉換為分割區。 此程序會讓回寫資料表變成新分割區的事實資料表。  
  
> [!CAUTION]  
>  不正確地使用分割區會造成不正確的 Cube 資料。 如需詳細資訊，請參閱 [建立及管理本機分割區 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)。  
  
 將回寫資料表轉換為分割區也會造成禁止寫入分割區。 分割區之資料格的所有未限制讀取/寫入原則和讀取/寫入權限會停用，且使用者將無法變更已顯示的 Cube 資料。 (已停用未限制讀取/寫入原則或已停用讀取/寫入權限的使用者仍然可以瀏覽 Cube)。讀取和意外讀取權限不受影響。  
  
 若要將回寫資料轉換為資料分割，請使用 [轉換為資料分割] 對話方塊，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，以滑鼠右鍵按一下可寫入資料分割的回寫資料表，即可存取此對話方塊。 您可以指定分割區的名稱，以及是否要在建立分割區的同時或稍後設計分割區的彙總。 若要在您選擇分割區的同時建立彙總，您必須選擇從現有的分割區複製彙總設計。 這通常 (但並非一定) 是目前的回寫分割區。 您也可以選擇在建立分割區的同時處理分割區。  
  
## <a name="see-also"></a>請參閱  
 [可寫入的資料分割](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions.md)   
 [啟用回寫到 OLAP Cube 在 Excel 2010 中的資料格層級](http://go.microsoft.com/fwlink/p/?LinkId=394952)   
 [啟用及設定安全性與 Analysis Services 回寫資料輸入](http://go.microsoft.com/fwlink/p/?LinkId=394953)  
  
  
