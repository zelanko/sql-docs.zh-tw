---
title: 遠端資料分割-進階設定對話方塊 (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.advancedrestoresettings.f1
ms.assetid: a03bb7e1-efaf-47c8-b0ee-f3e4438311cb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7677776bb1adf21d3234f770a9e2941edfa70ed0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074928"
---
# <a name="remote-partitions---advanced-settings-dialog-box-analysis-services---multidimensional-data"></a>遠端資料分割 - 進階設定對話方塊 (Analysis Services - 多維度資料)
  使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的 [遠端資料分割 - 進階設定] 對話方塊，即可編輯進階設定，例如代表維護遠端資料分割之遠端 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫的資料來源連接字串；另外使用 [還原資料庫] 對話方塊即可從遠端備份檔案還原遠端資料分割到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫。 在選取 [還原遠端資料分割] 選項之後，按一下遠端資料分割的省略符號按鈕 (**...**)，即可從 [還原資料庫] 對話方塊的 [資料分割] 頁面顯示 [遠端資料分割 - 進階設定] 對話方塊。  
  
## <a name="options"></a>選項。  
  
|詞彙|定義|  
|----------|----------------|  
|**資料來源名稱**|顯示資料來源的名稱，這代表管理所列出遠端資料分割的遠端 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫。|  
|**[備份檔案]**|顯示遠端備份檔案的名稱，其中包含所列出遠端資料分割要還原的資料。<br /><br /> 注意： 不會顯示備份檔案中指定遠端備份檔案，如果**備份檔案**上的資料行**分割區**頁面**Restore Database**  對話方塊。|  
|**連接字串**|顯示 [資料來源名稱] 中顯示之資料來源的連接字串。|  
|**編輯**|按一下即可顯示 [資料連結屬性] 對話方塊，並編輯連接字串中包含的屬性。|  
|**資料分割清單**|選取即可指定還原遠端資料分割的不同位置。 請注意，如果此位置並非在 Cube 中為該遠端資料分割指定的預設位置，則您只能變更遠端資料分割的還原資料夾。 下列方格 (選取此選項時啟用) 會用來指定每個遠端資料分割的還原資料夾：<br /><br /> **Cube**： 會顯示包含遠端資料分割的 cube 名稱。<br /><br /> **MeasureGroup**： 顯示包含遠端資料分割的量值群組的名稱。<br /><br /> **資料分割**： 顯示遠端資料分割的名稱。<br /><br /> **大小 (MB)**： 顯示的大小，以 mb 為單位，遠端資料分割。<br /><br /> **原始資料夾**： 會顯示在其中儲存遠端資料分割的原始資料夾名稱。<br /><br /> **還原資料夾**： 鍵入遠端資料分割，還原資料夾名稱，或按一下省略符號按鈕 (**...**) 以顯示**瀏覽遠端資料夾**對話方塊並選取要使用的資料夾路徑。 如需 [瀏覽遠端資料夾] 對話方塊的詳細資訊，請參閱[瀏覽遠端資料夾對話方塊 &#40;Analysis Services - 多維度資料&#41;](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services Designers and Dialog Boxes&#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [資料分割&#40;還原資料庫對話方塊&#41; &#40;Analysis Services-多維度資料&#41;](partitions-restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [備份與還原 Analysis Services 資料庫](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
