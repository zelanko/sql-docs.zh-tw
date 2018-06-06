---
title: 分析表格式模型在 Excel 中的 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1db764052a9c3370554a6456dc005612a2e8b95
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="analyze-a-tabular-model-in-excel"></a>分析在 Excel 中的表格式模型  
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的 [在 Excel 中進行分析] 功能會開啟 Microsoft Excel、建立模型工作空間資料庫的資料來源連接，以及將樞紐分析表加入工作表。 模型物件 (資料表、資料行、量值、階層和 KPI) 會包含在樞紐分析表欄位清單中當做欄位。  
  
> [!NOTE]  
>  為了使用 [在 Excel 中進行分析] 功能，您必須在與 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]相同的電腦上安裝 Microsoft Office 2003 或更高版本。 如果未將 Office 安裝在相同的電腦上，您可以在其他電腦上使用 Excel，然後連接至模型工作空間資料庫當做資料來源。 然後即可手動將樞紐分析表加入工作表。 模型物件 (資料表、資料行、量值及 KPI) 會包含在樞紐分析表欄位清單中當做欄位。  
  
## <a name="tasks"></a>工作  
  
#### <a name="to-analyze-a-tabular-model-project-by-using-the-analyze-in-excel-feature"></a>若要使用在 Excel 中進行分析功能來分析表格式模型專案  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，按一下 **[模型]** 功能表，然後按一下 **[在 Excel 中進行分析]**。  
  
2.  在 **[選擇認證和檢視方塊]** 對話方塊中，選取下列其中一個認證選項，以連接至模型工作空間資料來源：  
  
    -   若要使用目前的使用者帳戶，請選取 **[目前的 Windows 使用者]**。  
  
    -   若要使用其他使用者帳戶，請選取 **[其他 Windows 使用者]**。  
  
         此使用者帳戶通常是角色的成員。 不需要密碼。 只能在工作空間資料庫的 Excel 連接環境中使用此帳戶。  
  
    -   若要使用安全性角色，請選取 **[角色]**，然後在清單方塊中選取一個或多個角色。  
  
         您必須使用角色管理員定義安全性角色。 如需詳細資訊，請參閱[建立及管理角色](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)。  
  
3.  若要使用檢視方塊，請在 **[檢視方塊]** 清單方塊中選取檢視方塊。  
  
     您必須使用 [檢視方塊] 對話方塊定義檢視方塊 (非預設值)。 如需詳細資訊，請參閱[建立和管理檢視方塊](../../analysis-services/tabular-models/create-and-manage-perspectives-ssas-tabular.md)。  
  
> [!NOTE]  
>  當您在模型設計師中變更模型專案時，Excel 的樞紐分析表欄位清單不會自動重新整理。 若要重新整理樞紐分析表欄位清單，請在 Excel 的 **[選項]** 功能區上，按一下 **[重新整理]**。  
  
## <a name="see-also"></a>另請參閱  
 [在 Excel 中進行分析](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)  
  
  
