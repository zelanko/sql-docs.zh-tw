---
title: 管理模型（SQL Server 資料採礦增益集） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
ms.openlocfilehash: 6d5f0619e7291cc08b1750c0b35f9639cb7a9872
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66078043"
---
# <a name="manage-models-sql-server-data-mining-add-ins"></a>管理模型 (SQL Server 資料採礦增益集)
  ![資料採礦功能區中的管理模型按鈕](media/dmc-manage.gif "資料採礦功能區中的管理模型按鈕")  
  
 [**管理模型**] 對話方塊可讓您與目前所連接之[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]伺服器中儲存的現有「採礦模型」和「採礦結構」進行互動。 您也可以檢視及管理目前工作階段期間已建立的暫時性結構和模型。 如果您已使用工作階段模型和伺服器上儲存的模型，對話方塊中會顯示這兩種模型。  
  
## <a name="using-the-manage-models-wizard"></a>使用管理模型精靈  
 當您按一下 [**管理模型**] 時，會開啟 [**管理採礦結構和模型**] 對話方塊，提供下列功能的存取權來管理現有的資料採礦模型和結構：  
  
-   重新命名採礦模型或結構  
  
-   刪除採礦模型或結構  
  
-   清除採礦模型或結構  
  
-   使用新的或現有的資料來處理採礦結構  
  
-   匯出或匯入採礦模型或結構  
  
> [!NOTE]  
>  您無法使用這個對話方塊建立查詢或模型。 若要建立新的採礦結構，請使用適用于 Excel 的資料採礦用戶端中提供的其中一個嚮導，或使用**資料採礦查詢進階編輯器**。  
  
### <a name="requirements"></a>需求  
 若要管理資料採礦模型，您必須先建立與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接。 即使您使用儲存在暫存檔中的工作階段模型，還是需要連接。 如需有關如何建立或變更連接的詳細資訊，請參閱[連接到來源資料 &#40;適用于 Excel&#41;的資料採礦用戶端](connect-to-source-data-data-mining-client-for-excel.md)。  
  
 如果您連接的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體沒有包含任何現有的資料採礦結構或資料採礦模型，您可以使用精靈或此增益集提供的其他工具來建立它們。 您也可以使用**資料採礦模型進階編輯器**建立新的模型。  
  
## <a name="see-also"></a>另請參閱  
 [記載 &#40;適用于 Excel 的資料採礦增益集&#41;的採礦模型](documenting-mining-models-data-mining-add-ins-for-excel.md)   
 [&#40;適用于 Excel 的資料採礦增益集部署和調整採礦模型&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)   

  
