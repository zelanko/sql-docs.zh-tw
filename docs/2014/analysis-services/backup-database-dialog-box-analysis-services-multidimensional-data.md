---
title: 備份資料庫對話方塊 (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.Backup.f1
ms.assetid: 7811ce7d-6c37-4189-bfa6-ef36fb4932db
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a99ce67c4b42cc1def10127c8b1862a859d20723
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66064374"
---
# <a name="backup-database-dialog-box-analysis-services---multidimensional-data"></a>備份資料庫對話方塊 (Analysis Services - 多維度資料)
  透過 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的 [備份資料庫] 對話方塊，即可使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 備份檔 (.abf) 格式，將 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫備份至備份檔案中。  
  
> [!IMPORTANT]  
>  對於每個備份檔案，執行備份命令的使用者必須擁有寫入針對每個檔案所指定之備份位置的權限。 此外，使用者必須具有下列其中一個角色： [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體之伺服器角色的成員，或在即將備份之資料庫上擁有「完整控制 (系統管理員)」權限的資料庫角色成員。  
  
 **若要顯示 備份資料庫對話方塊**  
  
-   在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中，以滑鼠右鍵按一下 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的 [資料庫] 資料夾或物件總管中的資料庫，然後按一下 [備份]。  
  
## <a name="options"></a>選項。  
 **指令碼**  
 根據在對話方塊中選取的選項，建立備份指令碼。 此還原指令碼是以 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 指令碼語言 (ASSL) 撰寫而成。  
  
 依預設，按一下**指令碼**圖示就會將備份指令碼傳送至新的查詢視窗中。  
  
 按一下 [指令碼] 箭號就會顯示功能表，讓您選擇要傳送備份指令碼的目標位置：  
  
-   傳送到新的查詢視窗 (預設值)。  
  
-   傳送到檔案。  
  
-   傳送到剪貼簿。  
  
-   傳送到作業。  
  
 **[資料庫備份]**  
 顯示目前選取的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫名稱。  
  
 **[備份檔案]**  
 鍵入要使用的備份檔案之完整路徑和檔案名稱。  
  
 **瀏覽**  
 按一下即可顯示 [另存新檔] 對話方塊，並選取要使用的備份檔案之路徑和檔案名稱。 如需 [另存新檔] 對話方塊的詳細資訊，請參閱[另存新檔對話方塊 &#40;Analysis Services - 多維度資料&#41;](save-file-as-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **允許檔案覆寫**  
 選取即可覆寫現有的備份檔案或遠端備份檔案 (如果有的話)。  
  
> [!NOTE]  
>  如果未選取此選項，且 [備份檔案] 中指定的備份檔案或 [遠端備份檔案] 中指定的遠端備份檔案存在的話，就會發生錯誤。  
  
 **套用壓縮**  
 選取即可壓縮備份檔案的內容，如果指定的話，也會壓縮遠端備份檔案的內容。  
  
 **加密備份檔案**  
 選取即可使用 [密碼] 中提供的密碼，為備份檔案加密。  
  
 **密碼**  
 鍵入加密備份檔案時使用的密碼，如果指定的話，也會適用於遠端備份檔案的加密。  
  
> [!NOTE]  
>  唯有選取了 [加密備份檔案] 時，才會啟用此選項。  
  
 **確認密碼**  
 鍵入 [密碼] 中輸入的密碼，以確認備份檔案的密碼，如果指定的話，也會適用於遠端備份檔案的密碼。  
  
> [!NOTE]  
>  唯有選取了 [加密備份檔案] 時，才會啟用此選項。  
  
 **備份遠端資料分割**  
 選取即可在備份檔案中，包含位置資訊和遠端資料分割的資料。  
  
> [!NOTE]  
>  只有目前選取的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫有使用遠端資料分割時，才會啟用此選項。  
  
 **遠端資料分割備份位置**  
 顯示與所選取資料庫相關聯的遠端資料分割位置，以及用來備份遠端資料分割的資料和中繼資料之遠端備份檔案。 下列是可使用的資料行：  
  
|「資料行」|描述|  
|------------|-----------------|  
|**Server**|顯示管理遠端資料分割的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體。|  
|**[資料庫備份]**|顯示包含遠端資料分割的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫。|  
|**資料分割清單**|顯示 [資料庫] 中顯示的資料庫，所包含的遠端資料分割清單。|  
|**遠端備份檔案**|鍵入要使用的遠端備份檔案之完整路徑和檔案名稱；或按一下省略符號按鈕 (**...**) 來顯示 [另存新檔] 對話方塊，並選取要使用的遠端備份檔案之路徑和檔案名稱。 如需 [另存新檔] 對話方塊的詳細資訊，請參閱[另存新檔對話方塊 &#40;Analysis Services - 多維度資料&#41;](save-file-as-dialog-box-analysis-services-multidimensional-data.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services Designers and Dialog Boxes&#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [備份與還原 Analysis Services 資料庫](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
