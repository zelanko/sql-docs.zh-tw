---
title: 修改或刪除 Analysis Services 資料庫 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], modifying
- removing databases
- deleting databases
- dropping databases
- databases [Analysis Services], deleting
- modifying databases
ms.assetid: e48e3988-c091-4379-aabc-4da62f709a7e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1bcb8d635721a31429f387d135ed7b0bbf7112d6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48196778"
---
# <a name="modify-or-delete-an-analysis-services-database"></a>修改或刪除 Analysis Services 資料庫
  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的部署之前和在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的部署之後，您可以變更 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]資料庫的名稱和描述。 您也可以調整 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的其他設定，視環境而定。  
  
> [!NOTE]  
>  在線上模式中，您無法使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 來變更資料庫屬性。  
  
## <a name="modifying-databases-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 修改資料庫  
 在部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫之後，您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來變更 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在連接到資料庫所包含的資料來源時所使用的模擬模式。 嘗試連接到資料來源以供處理、瀏覽或鑽研時，模擬模式可以讓您指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用的安全性內容。  
  
## <a name="modifying-databases-using-sql-server-data-tools"></a>使用 SQL Server Data Tools 修改資料庫  
 在專案模式中，您可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ，修改用來定義資料庫之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的標題和描述的翻譯。 如需有關使用中的翻譯[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫，請參閱[Analysis Services 多維度的全球化案例](../globalization-scenarios-for-analysis-services-multiidimensional.md)。  
  
 在資料庫所包含的維度中，您可以設定與帳戶屬性所使用之帳戶類型相關聯的別名和彙總函式。 針對帳戶圖表中的帳戶類型，別名可讓您選取組織所使用的特定商業用語。 帳戶屬性的成員會使用帳戶類型，指出如何使用資料庫包含的每一個帳戶類型所指定的彙總函式，以彙總每一個成員的量值。 如需帳戶屬性的詳細資訊，請參閱 [屬性和屬性階層](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)。  
  
## <a name="deleting-databases"></a>刪除資料庫  
 刪除現有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫會刪除資料庫和資料庫中所有的 Cube、維度以及採礦模型。 您只能刪除 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中現有的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]資料庫。  
  
#### <a name="to-delete-an-analysis-services-database"></a>若要刪除 Analysis Services 資料庫  
  
1.  連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。  
  
2.  在 [物件總管] 中，展開所連接之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的節點，並確定可以看見要刪除的物件。  
  
3.  以滑鼠右鍵按一下要刪除的物件，並選取 [刪除]。  
  
4.  在 **[刪除物件]** 對話方塊中，按一下 **[確定]**。  
  
## <a name="see-also"></a>另請參閱  
 [記錄和編寫 Analysis Services 資料庫的指令碼](document-and-script-an-analysis-services-database.md)  
  
  
