---
title: 管理模型 （SQL Server 資料採礦增益集） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, importing
- mining models, deleting
- mining models, managing
- mining models, training
- mining models, processing
- mining models, exporting
ms.assetid: c11380f0-7c24-4668-9cdf-9c53e4aff665
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cb7fee7425db1e22cd8db59477fb0bf30ce1d01c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48225368"
---
# <a name="manage-models-sql-server-data-mining-add-ins"></a>管理模型 (SQL Server 資料採礦增益集)
  ![管理模型 按鈕，資料採礦功能區](media/dmc-manage.gif "管理模型] 按鈕，[資料採礦功能區")  
  
 **管理模型**對話方塊可讓您與現有的採礦模型和採礦結構儲存在互動[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]目前連接的伺服器。 您也可以檢視及管理目前工作階段期間已建立的暫時性結構和模型。 如果您已使用工作階段模型和伺服器上儲存的模型，對話方塊中會顯示這兩種模型。  
  
## <a name="using-the-manage-models-wizard"></a>使用管理模型精靈  
 當您按一下 **管理模型**，則**管理採礦結構和模型**對話方塊隨即開啟，提供下列功能來管理現有的資料採礦模型和結構的存取權：  
  
-   重新命名採礦模型或結構  
  
-   刪除採礦模型或結構  
  
-   清除採礦模型或結構  
  
-   使用新的或現有的資料來處理採礦結構  
  
-   匯出或匯入採礦模型或結構  
  
> [!NOTE]  
>  您無法使用這個對話方塊建立查詢或模型。 若要建立新的採礦結構，使用其中一種 Excel，或使用資料採礦用戶端所提供的精靈**資料採礦進階查詢編輯器**。  
  
### <a name="requirements"></a>需求  
 若要管理資料採礦模型，您必須先建立與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接。 即使您使用儲存在暫存檔中的工作階段模型，還是需要連接。 如需如何建立或變更連線的詳細資訊，請參閱[連接至來源的資料&#40;適用於 Excel 的資料採礦用戶端&#41;](connect-to-source-data-data-mining-client-for-excel.md)。  
  
 如果您連接的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體沒有包含任何現有的資料採礦結構或資料採礦模型，您可以使用精靈或此增益集提供的其他工具來建立它們。 您也可以藉由建立新的模型**資料採礦進階查詢編輯器**。  
  
## <a name="see-also"></a>另請參閱  
 [記錄採礦模型&#40;資料採礦適用於 Excel 的增益集&#41;](documenting-mining-models-data-mining-add-ins-for-excel.md)   
 [部署及調整採礦模型&#40;資料採礦適用於 Excel 的增益集&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)   

  
