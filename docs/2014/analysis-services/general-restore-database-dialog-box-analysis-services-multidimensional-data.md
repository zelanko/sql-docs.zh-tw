---
title: 一般（還原資料庫對話方塊）（Analysis Services-多維度資料） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.restoredbdialog.f1
ms.assetid: 319e7ef5-c9c7-4e50-8690-02a90aed006f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2ebc1bc72a15545412adcc71d10feb08f3f05b16
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66080949"
---
# <a name="general-restore-database-dialog-box-analysis-services---multidimensional-data"></a>一般 (還原資料庫對話方塊) (Analysis Services - 多維度資料)
  在 **中，使用** [還原資料庫] **對話方塊的** [一般] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 頁面，即可指定在還原 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫時使用的備份檔案和一般設定。  
  
> [!IMPORTANT]  
>  對於每個備份檔案，執行還原命令的使用者必須擁有從針對每個檔案所指定之備份位置讀取的權限。 若要還原沒有安裝在伺服器上的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫，使用者也必須是該 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體之伺服器角色的成員。 若要覆寫 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫，使用者必須具有下列其中一個角色： [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體之伺服器角色的成員，或在即將還原之資料庫上擁有「完整控制 (系統管理員)」權限的資料庫角色成員。  
  
> [!NOTE]  
>  還原現有的資料庫之後，還原資料庫的使用者可能會喪失已還原資料庫的存取權。 如果在執行備份時，使用者不是伺服器角色的成員，也不是擁有完整控制權 (管理員) 權限的資料庫角色成員，就可能會發生存取權喪失的情況。  
  
 **在還原資料庫對話方塊中顯示一般頁面**  
  
-   在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中，以滑鼠右鍵按一下 ** 執行個體的 [資料庫]**[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料夾或物件總管**** 中的資料庫、按一下 [還原]****，然後按一下 [選取頁面]**** 底下的 [一般]****。  
  
## <a name="options"></a>選項。  
 **文字**  
 根據在對話方塊中選取的選項，建立還原指令碼。 此還原指令碼是以 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 指令碼語言 (ASSL) 撰寫而成。  
  
 根據預設，按一下 **[指令碼]** 圖示就會將還原指令碼傳送至新的查詢視窗中。  
  
 按一下 **[指令碼]** 箭號就會顯示功能表，讓您選擇要傳送還原指令碼的目標位置：  
  
-   傳送到新的查詢視窗 (預設值)。  
  
-   傳送到檔案。  
  
-   傳送到剪貼簿。  
  
-   傳送到作業。  
  
 **還原資料庫**  
 選取要還原的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫。  
  
 **從備份檔案**  
 選取備份檔案，從該備份檔案中還原選取的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫。  
  
 **瀏覽**  
 按一下即可顯示 [尋找資料庫檔案]**** 對話方塊，並選取要使用之備份檔案的路徑和檔案名稱。 如需 [尋找資料庫檔案]**** 對話方塊的詳細資訊，請參閱[尋找資料庫檔案對話方塊 &#40;Analysis Services - 多維度資料&#41;](locate-database-files-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **允許資料庫覆寫**  
 選取即可允許 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 還原所選取備份檔案的內容，並覆寫所選取 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫中的任何現有物件。  
  
 **包含安全性資訊**  
 選取即可複製備份檔案中儲存的任何安全性資訊至 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫。  
  
 如果選取此選項，您就可以從選取此選項所啟用的下拉式清單中，選擇安全性資訊的數量。 有下列選項可供使用：  
  
|選項|描述|  
|------------|-----------------|  
|**全部複製**|還原備份檔案包含的資料庫角色，以及角色相關聯的使用者帳戶。|  
|**略過成員資格**|還原備份檔案包含的資料庫角色，但不還原角色相關聯的使用者帳戶。|  
  
 **密碼**  
 如果備份檔案已加密，請鍵入用來加密備份檔案的密碼。  
  
## <a name="see-also"></a>另請參閱  
 [[還原資料庫] 對話方塊 &#40;Analysis Services-多維度資料&#41;](restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [分割區 &#40;[還原資料庫] 對話方塊&#41; &#40;Analysis Services 多維度資料&#41;](partitions-restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [備份與還原 Analysis Services 資料庫](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
