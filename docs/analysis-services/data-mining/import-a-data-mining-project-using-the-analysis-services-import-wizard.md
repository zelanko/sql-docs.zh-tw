---
title: 匯入資料採礦專案，使用 Analysis Services 匯入精靈 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 52e98d6916b66c4ab26b2791d023d25bffc4cab8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63043956"
---
# <a name="import-a-data-mining-project-using-the-analysis-services-import-wizard"></a>使用 Analysis Services 匯入精靈匯入資料採礦專案
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  本主題描述如何在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中使用 [從伺服器匯入 (多維度和資料採礦)] 範本，從另一部伺服器上的現有資料採礦專案匯入中繼資料來建立新的資料採礦專案。  
  
## <a name="import-data-sources-mining-structures-and-mining-models-from-an-existing-data-mining-project"></a>從現有的資料採礦專案匯入資料來源、採礦結構和採礦模型  
 當您使用 [從伺服器匯入 (多維度和資料採礦)] 範本時，[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會建立新的資料採礦專案，然後從指定的資料採礦專案複製中繼資料。 新的專案所包含的資料來源、資料來源檢視、採礦結構和採礦模型與您匯入的來源 ssASnoversion 資料庫相同。 但是，要等到您依照以下所述的內容更新某些屬性及處理物件之後，才能使用專案：  
  
-   資料本身不會複製從來源伺服器到新的資料採礦專案僅匯入資料來源和資料來源檢視的定義。 因此，當您完成匯入程序及建立物件之後，您必須定型採礦結構和相依模型來以資料擴展物件。 您可以使用資料採礦設計師中的 **[全部處理]** 命令來定型模型和結構。  
  
-   如果您正在匯入之前在舊版 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中所建立的專案，則資料來源可能會使用匯入專案之目標伺服器上所未安裝的提供者。 如果您在處理匯入的採礦結構時遇到錯誤，請以滑鼠右鍵按一下每一個資料來源，然後選取 [開啟設計工具] 來編輯連接字串，並檢閱提供者屬性。  
  
     此時您也可能需要確認，您用來處理資料採礦物件或查詢資料採礦模型的帳戶擁有資料來源的必要權限。  
  
-   根據預設，當您匯入專案時，工作空間資料庫會設定為 localhost，或是預設執行個體會在 **中設定為** [預設的目標伺服器] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。 若要設定這個屬性，請從 **[選項]** 功能表選取 **[商業智慧設計師]**，再選取 **[Analysis Services]**，然後選取 **[一般]**。  
  
     請注意在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，可設定另一個單獨的選項來設定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格式模型專案的預設部署伺服器。 **[預設部署伺服器]** 設定會決定表格式模型專案的預設工作空間資料庫。 您不能使用可支援資料採礦專案之表格式模型的執行個體。  
  
     如果您無法變更預設部署資料庫來使用在多維度或資料採礦模式中執行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，您可以隨時使用 **[專案屬性]** 對話方塊來指定部署資料庫。  
  
#### <a name="to-create-a-new-data-mining-project-by-importing-an-existing-data-mining-project"></a>若要匯入現有的資料採礦專案來建立新的資料採礦專案  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]的 **[檔案]** 功能表上，按一下 **[新增]**，然後再按一下 **[專案]**。  
  
2.  在 [新增專案] 對話方塊的 [已安裝的範本] 底下，按一下 [商業智慧]，再按一下 [Analysis Services]，然後按一下 [從伺服器匯入 (多維度和資料採礦)]。  
  
3.  在 **[名稱]** 中，輸入專案的名稱，並指定位置和方案名稱，然後按一下 **[確定]**。  
  
     **[匯入 Analysis Services 資料庫精靈]** 隨即啟動。 在歡迎頁面上按一下 [確定]，繼續進行。  
  
4.  在 **[選取來源資料庫]** 頁面上，針對 **[伺服器]** 指定包含您想要匯入之方案的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。  
  
     針對 **[資料庫]** 選擇包含您想要匯入之資料採礦物件的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。  
  
    > [!WARNING]  
    >  您不能指定您想要匯入的物件；當您選擇現有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫時，所有多維度和資料採礦物件都會匯入。  
  
     按一下 [下一步] 。  
  
5.  **[正在完成精靈]** 頁面會顯示匯入作業的進度。 您不能取消此作業或是變更正在匯入的物件。 完成時按一下 **[完成]** 。  
  
     隨即使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]自動開啟新的專案。  
  
## <a name="see-also"></a>另請參閱  
 [專案屬性](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)  
  
  
