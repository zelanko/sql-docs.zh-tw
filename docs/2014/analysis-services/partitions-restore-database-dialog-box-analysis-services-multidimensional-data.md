---
title: 資料分割 （還原資料庫對話方塊） (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.restoredbdialog.partitions.f1
ms.assetid: 1ad4dde5-4651-4069-875c-7ab73cd8b4f4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a0c28420d711fd009dfc2b1e36ef4a613b3ecfaf
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66072108"
---
# <a name="partitions-restore-database-dialog-box-analysis-services---multidimensional-data"></a>資料分割 (還原資料庫對話方塊) (Analysis Services - 多維度資料)
  在 **中，使用** [還原資料庫] **對話方塊的** [資料分割] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 頁面，即可指定本機資料分割的還原位置和是否還原遠端資料分割，以及指定還原遠端資料分割時所使用的遠端備份檔案。  
  
> [!IMPORTANT]  
>  對於每個備份檔案，執行還原命令的使用者必須擁有從針對每個檔案所指定之備份位置讀取的權限。 若要還原沒有安裝在伺服器上的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫，使用者也必須是該 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體之伺服器角色的成員。 若要覆寫 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫，使用者必須具有下列其中一個角色： [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體之伺服器角色的成員，或在即將還原之資料庫上擁有完整控制權 (管理員) 權限的資料庫角色成員。  
  
> [!NOTE]  
>  還原現有的資料庫之後，還原資料庫的使用者可能會喪失已還原資料庫的存取權。 如果在執行備份時，使用者不是伺服器角色的成員，也不是擁有完整控制權 (管理員) 權限的資料庫角色成員，就可能會發生存取權喪失的情況。  
  
 **若要在還原資料庫 對話方塊中顯示資料分割頁面**  
  
-   在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中，以滑鼠右鍵按一下 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的 [資料庫] 資料夾或物件總管中的資料庫，按一下 [還原]，然後按一下 [選取頁面] 底下的 [資料分割]。  
  
## <a name="options"></a>選項。  
 **指令碼**  
 根據在對話方塊中選取的選項，建立還原指令碼。 此還原指令碼是以 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 指令碼語言 (ASSL) 撰寫而成。  
  
 根據預設，按一下 **[指令碼]** 圖示就會將還原指令碼傳送至新的查詢視窗中。  
  
 按一下 **[指令碼]** 箭號就會顯示功能表，讓您選擇要傳送還原指令碼的目標位置：  
  
-   傳送到新的查詢視窗 (預設值)。  
  
-   傳送到檔案。  
  
-   傳送到剪貼簿。  
  
-   傳送到作業。  
  
 **還原至原始位置**  
 選取即可將備份檔案包含的本機資料分割，還原至它們的原始位置。  
  
 **選取不同的位置**  
 選取即可指定不同的位置，來還原本機資料分割。  
  
> [!NOTE]  
>  唯有對 Cube 中的資料分割指定預設位置以外的位置時，您才能變更本機資料分割的還原資料夾。  
  
 下列方格會在選取此選項之後啟用，它是用來指定每一個本機資料分割的還原資料夾：  
  
|「資料行」|描述|  
|------------|-----------------|  
|**Cube**|顯示包含本機資料分割的 Cube 名稱。|  
|**MeasureGroup**|顯示包含本機資料分割之量值群組的名稱。|  
|**資料分割**|顯示本機資料分割的名稱。|  
|**大小 (MB)**|顯示本機資料分割的大小，以 MB 為單位。|  
|**原始資料夾**|顯示儲存本機資料分割之原始資料夾的名稱。|  
|**還原資料夾**|輸入本機資料分割的還原資料夾名稱，或按一下省略符號按鈕 (**...**)，以顯示 [瀏覽遠端資料夾] 對話方塊並選取要使用的資料夾路徑。 如需 [瀏覽遠端資料夾] 對話方塊的詳細資訊，請參閱[瀏覽遠端資料夾對話方塊 &#40;Analysis Services - 多維度資料&#41;](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md)。|  
  
 **還原遠端資料分割**  
 選取即可還原遠端備份檔案中儲存的遠端資料分割。  
  
> [!NOTE]  
>  只有在備份檔案包含遠端資料分割的參考時，才會啟用此選項。  
  
 下列方格會在選取此選項之後啟用，它是用來指定每一個本機資料分割的還原資料夾：  
  
|「資料行」|描述|  
|------------|-----------------|  
|**Server**|顯示管理遠端資料分割的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體名稱。|  
|**資料來源**|顯示備份檔案中的資料來源名稱，此資料來源代表包含遠端資料分割的資料庫。|  
|**備份檔案**|輸入要使用之遠端備份檔案的完整路徑和檔案名稱，或按一下省略符號按鈕 (**...**)，以顯示 [尋找資料庫檔案] 對話方塊並選取要使用之遠端備份檔案的路徑和檔案名稱。 如需 [尋找資料庫檔案] 對話方塊的詳細資訊，請參閱[尋找資料庫檔案對話方塊 &#40;Analysis Services - 多維度資料&#41;](locate-database-files-dialog-box-analysis-services-multidimensional-data.md)。|  
|**...**|按一下即可顯示 [遠端資料分割 - 進階設定] 對話方塊，並修改還原遠端資料分割的進階選項，例如資料來源的連接字串。 如需 [遠端資料分割 - 進階設定] 對話方塊的詳細資訊，請參閱[遠端資料分割 - 進階設定對話方塊 &#40;Analysis Services - 多維度資料&#41;](remote-partitions-advanced-settings-dialog-analysis-services-multidimensional-data.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [還原資料庫對話方塊 &#40;Analysis Services - 多維度資料&#41;](restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [一般&#40;還原資料庫對話方塊&#41; &#40;Analysis Services-多維度資料&#41;](general-restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [備份與還原 Analysis Services 資料庫](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
