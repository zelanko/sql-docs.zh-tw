---
title: 還原選項 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], restoring
- restoring databases [Analysis Services]
ms.assetid: 75c73802-f321-4671-afc7-54505d62c013
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 348e3254cb31cfef72e40b35ac74cbe9cf578834
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48060360"
---
# <a name="restore-options"></a>還原選項
  有許多方法可以還原 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫，所有的方法都需要您具備伺服器電腦和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的管理員權限。 若要還原 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫，您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中開啟 [還原資料庫] 對話方塊，選取適當的選項組態，然後從對話方塊執行還原。 或者，您可以使用檔案中已經指定的設定來建立指令碼；然後儲存指令碼並視需要執行。 如此即可使用 XMLA 來完成還原，如下節中的描述。  
  
## <a name="restoring-databases-using-xmla"></a>使用 XMLA 還原資料庫  
 XMLA Restore 命令是依據 .abf 檔案執行還原，以自動化還原處理序的方法。 Restore 命令有數個屬性可供設定，以指定安全性定義、儲存遠端資料分割的位置，以及關聯式 OLAP (ROLAP) 物件的重新放置。 如需詳細資訊，請參閱 <<c0> [ 還原的項目&#40;XMLA&#41;](../xmla/xml-elements-commands/restore-element-xmla.md)。</c0>  
  
> [!IMPORTANT]  
>  對於每個備份檔案，執行還原命令的使用者必須擁有從針對每個檔案所指定之備份位置讀取的權限。 若要還原沒有安裝在伺服器上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫，使用者也必須是該 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體之伺服器角色的成員。 若要覆寫 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫，使用者必須具有下列其中一個角色： [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體之伺服器角色的成員，或在即將還原之資料庫上擁有「完整控制 (系統管理員)」權限的資料庫角色成員。  
  
> [!NOTE]  
>  還原現有的資料庫之後，還原資料庫的使用者可能會喪失已還原資料庫的存取權。 如果在執行備份時，使用者不是伺服器角色的成員，也不是擁有完整控制權 (管理員) 權限的資料庫角色成員，就可能會發生存取權喪失的情況。  
  
## <a name="see-also"></a>另請參閱  
 [還原資料庫對話方塊&#40;Analysis Services-多維度資料&#41;](../restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [備份與還原 Analysis Services 資料庫](backup-and-restore-of-analysis-services-databases.md)   
 [Restore 元素&#40;XMLA&#41;](../xmla/xml-elements-commands/restore-element-xmla.md)   
 [備份、 還原和同步處理資料庫&#40;XMLA&#41;](../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)  
  
  
