---
title: 還原資料庫對話方塊 (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.Restore.f1
ms.assetid: a3990d47-55e2-424e-8eac-87edc937e806
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 42649fd9fe8284e89aebd37c2d9b668a3ac34a2f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66070255"
---
# <a name="restore-database-dialog-box-analysis-services---multidimensional-data"></a>還原資料庫對話方塊 (Analysis Services - 多維度資料)
  使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的 [還原資料庫] 對話方塊，即可從使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 備份檔案 (.abf) 格式的備份檔案還原 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫。  
  
> [!IMPORTANT]  
>  對於每個備份檔案，執行還原命令的使用者必須擁有從針對每個檔案所指定之備份位置讀取的權限。 若要還原沒有安裝在伺服器上的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫，使用者也必須是該 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體之伺服器角色的成員。 若要覆寫 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫，使用者必須具有下列其中一個角色： [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體之伺服器角色的成員，或在即將還原之資料庫上擁有完整控制權 (管理員) 權限的資料庫角色成員。  
  
> [!NOTE]  
>  還原現有的資料庫之後，還原資料庫的使用者可能會喪失已還原資料庫的存取權。 如果在執行備份時，使用者不是伺服器角色的成員，也不是擁有完整控制權 (管理員) 權限的資料庫角色成員，就可能會發生存取權喪失的情況。  
  
 **若要顯示 還原資料庫對話方塊**  
  
-   在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中，以滑鼠右鍵按一下 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的 [資料庫] 資料夾或**物件總管**中的資料庫，然後按一下 [還原]。  
  
 **[還原資料庫]** 對話方塊包含下列頁面。  
  
## <a name="pages"></a>頁面  
 **一般**  
 使用此頁面即可選取要還原的資料庫、用來還原資料庫的備份檔案，以及還原資料庫時使用的一般選項與密碼。 如需此頁面的詳細資訊，請參閱[一般 &#40;還原資料庫對話方塊&#41; &#40;Analysis Services – 多維度資料&#41;](general-restore-database-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **資料分割**  
 使用此頁面即可將本機資料分割還原至指定的位置，以及從遠端備份檔案還原遠端資料分割。 如需此頁面的詳細資訊，請參閱[資料分割 &#40;還原資料庫對話方塊&#41; &#40;Analysis Services – 多維度資料&#41;](partitions-restore-database-dialog-box-analysis-services-multidimensional-data.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services Designers and Dialog Boxes&#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [備份與還原 Analysis Services 資料庫](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
