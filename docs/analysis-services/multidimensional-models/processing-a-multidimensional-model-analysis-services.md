---
title: 處理 Analysis Services 多維度模型 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a6116019898e61cc414a14a05273a3f2839267a0
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072485"
---
# <a name="processing-a-multidimensional-model-analysis-services"></a>處理多維度模型 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  處理是一個步驟或是一連串的步驟，Analysis Services 會在這些步驟中將關聯式資料來源中的資料載入多維度模型中。 如果是使用 MOLAP 儲存的物件，資料會儲存至磁碟的資料庫檔案資料夾中。 對於 ROLAP 儲存，視需要發生處理，以回應物件的 MDX 查詢。 如果是使用 ROLAP 儲存的物件，處理是指在傳回查詢結果之前更新快取。  
  
 根據預設，當您將方案部署到伺服器時便會進行處理作業。 您也可以處理方案的全部或一部分，不論是透過類似 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]等工具隨選處理，還是透過 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和 SQL Server Agent 依排程處理。 當您對模型進行結構變更 (例如移除維度或變更其相容性層級) 時，您必須再次處理，以同步處理模型的實體和邏輯層面。  
  
 本主題包含下列各節：  
  
 [必要條件](#bkmk_prereq)  
  
 [選擇工具或方法](#bkmk_tool)  
  
 [處理物件](#bkmk_proc)  
  
 [Reprocessing Objects](#bkmk_reproc)  
  
##  <a name="bkmk_prereq"></a> 必要條件  
  
-   處理需要 Analysis Services 執行個體的管理權限。 如果您以互動方式從 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 或 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]處理，您必須是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上的伺服器管理員角色成員。 如果是自動執行的處理，例如使用透過 SQL Server Agent 排程的 SSIS 封裝，則用來執行此封裝的帳戶必須是伺服器管理員角色的成員。 如需設定管理員權限的詳細資訊，請參閱 [將伺服器管理員權限授與 Analysis Services 執行個體](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)。  
  
-   用來擷取資料的帳戶會在資料來源物件中指定，這會以模擬選項的形式 (如果您是使用 Windows 驗證) 或是連接字串中的使用者名稱形式 (如果是使用資料庫驗證) 指定。 該帳戶必須擁有模型所使用之關聯式資料來源的讀取權限。  
  
-   必須先部署專案或方案，然後才能處理任何物件。  
  
     一開始在模型開發的早期階段，部署和處理會一起進行。 但是，在您部署方案之後可以設定選項，以便於稍後處理模型。 如需部署的詳細資訊，請參閱[部署 Analysis Services 專案 &#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)。  
  
##  <a name="bkmk_tool"></a> 選擇工具或方法  
 您可以使用用戶端應用程式 (例如 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 或 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]) 以互動方式處理物件，或使用以 SQL Server Agent 作業或 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝方式執行之已編寫指令碼的作業。  
  
 根據模型是處於積極開發或實際執行狀態，處理資料庫的方式差別很大。 一旦模型部署至實際執行伺服器後，處理必須受到嚴格控制，以確保多維度資料的完整性和可用性。 因為物件彼此相依，處理通常在整個模型中有連鎖效應，其他物件也會一前一後處理或取消處理。 如果部分物件處於未處理的狀態，該資料的查詢將無法解析，而中斷使用該資料的任何報表或應用程式。 在開發處理生產資料庫的策略時，請考慮使用已偵錯及測試的指令碼或 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝，以避免運算子錯誤或步驟被忽略。  
  
 如需詳細資訊，請參閱[處理的工具和方式 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/tools-and-approaches-for-processing-analysis-services.md)。  
  
##  <a name="bkmk_proc"></a> 處理物件  
 處理會影響下列 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件：量值群組、資料分割、維度、Cube、採礦模型、採礦結構和資料庫。 當物件包含一個或多個物件時，處理最高層級物件會造成串聯處理所有較低層級物件。 例如，Cube 通常會包含一個或多個量值群組 (每一個量值群組又會包含一個或多個資料分割) 及維度。 處理 Cube 會使得 Cube 之內的所有量值群組以及目前處於尚未處理狀態的構成維度進行處理。 如需處理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的詳細資訊，請參閱 [處理 Analysis Services 物件](../../analysis-services/multidimensional-models/processing-analysis-services-objects.md)。  
  
 在處理作業進行的同時，受影響的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件可以存取進行查詢。 處理作業在交易之內進行，交易可以認可或回復。 如果處理作業失敗，就會回復該交易。 如果處理作業成功，在認可變更時，會在物件上放置獨佔鎖定，也就是說，物件會暫時無法進行查詢或處理。 在交易的認可階段期間，查詢仍可傳送至物件，但要等到完成認可之後，才會進入佇列。  
  
 在處理作業期間，物件是否已處理以及要如何處理，都依為該物件所設的處理選項而定。 如需可套用至每一個物件之特定處理選項的詳細資訊，請參閱[處理選項和設定 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)。  
  
##  <a name="bkmk_reproc"></a> Reprocessing Objects  
 包含未處理元素的 Cube 必須重新處理才能進行瀏覽。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的 Cube 包含量值群組和資料分割，必須先加以處理，才能查詢 Cube。 如果構成維度處於尚未處理的狀態，處理 Cube 會使得 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 處理 Cube 的構成維度。 第一次處理物件之後，如果有發生下列任一情況，則必須部分或完整地重新處理它：  
  
-   物件的結構變更，例如卸除事實資料表中的資料行。  
  
-   物件的彙總設計變更。  
  
-   需要更新物件中的資料。  
  
 當您在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中處理物件時，您可以選取處理選項，或啟用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 來決定適當的處理類型。 可用的處理方法會因不同物件而異，並會以物件類型為基礎。 另外，可用的方法也會依據物件上次處理之後所發生的變更而定。 如果您讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 自動選取處理方法，它將使用的方法是能夠使物件在最短時間內回到完整處理狀態。 如需詳細資訊，請參閱[處理選項和設定 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [邏輯架構 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [資料庫物件 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
