---
title: "AMO 概念和物件模型 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- AMO, classes
- Analysis Management Objects, classes
- objects [Analysis Management Objects]
- AMO, objects
- classes [AMO]
- AMO
- Analysis Management Objects
- Analysis Management Objects, objects
ms.assetid: 3b0cdf8e-46d5-4dfe-8b2c-233c27e1473e
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8cafbc9e41c5ee6af95721372f51361e11e1b1f5
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="amo-concepts-and-object-model"></a>AMO 概念和物件模型
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]本主題提供定義的 「 分析管理物件 」 (AMO) 中，AMO 如何與其他工具和文件庫中的架構提供相關[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，以及概念性地說明在 AMO 中的所有主要物件。  
  
 AMO 是 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 管理類別的完整集合，可在 Managed 環境中的 <xref:Microsoft.AnalysisServices> 命名空間之下，用程式設計方式使用它。 類別包括在 AnalysisServices.dll 檔案中，通常位於何處[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]安裝程式安裝檔案，在資料夾 \100\SDK\Assemblies\\。 若要使用 AMO 類別，請在專案中加入此組件的參考。  
  
 使用 AMO，您可以建立、 修改和刪除物件，例如 cube、 維度、 採礦結構和[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]資料庫; 高於所有這些物件可從您的應用程式在.NET Framework 執行動作。 您也可以處理和更新儲存在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫中的資訊。  
  
 您無法使用 AMO 查詢您的資料。 若要查詢您的資料，請使用[使用 ADOMD.NET 來開發](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)。  
  
 本主題包含下列幾節：  
  
 [AMO 中的 Analysis Services 架構](#AMOintheAnalysisServicesArchitecture)  
  
 [AMO 架構](#AMOArchitecture)  
  
 [使用 AMO](#bkmk_UsingAMO)  
  
 [使用 AMO 自動化管理工作](#AutomatingAdministrativeTaskswithAMO)  
  
##  <a name="AMOintheAnalysisServicesArchitecture"></a>AMO 中的 Analysis Services 架構  
 依設計，AMO 僅適用於物件管理，而不適用於查詢資料。 如果使用者需要查詢[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]用戶端應用程式中的資料，用戶端應用程式應該使用[使用 ADOMD.NET 來開發](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)。  
  
##  <a name="AMOArchitecture"></a>AMO 架構  
 AMO 是完整的設計來管理的執行個體的類別庫[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]從.NET Framework 2.0 版之下的 managed 程式碼中用戶端應用程式。  
  
 AMO 類別庫是以類別階層的方式設計，在階層中某些類別必須在其他類別之前先具現化，才能在程式碼中使用它們。 在程式碼中隨時都可以具現化輔助類別，但是您可能會先具現化一或多個階層類別，然後才使用任何一個輔助類別。  
  
 下圖是包括主要類別的 AMO 階層之高階檢視。 此圖顯示類別在其容器及其對等之間的位置。 <xref:Microsoft.AnalysisServices.Dimension> 屬於 <xref:Microsoft.AnalysisServices.Database> 和 <xref:Microsoft.AnalysisServices.Server>，而且可以與 <xref:Microsoft.AnalysisServices.DataSource> 和 <xref:Microsoft.AnalysisServices.MiningStructure> 同時建立。 您必須先具現化某些對等類別，才可以使用其他類別。 例如，您必須建立 <xref:Microsoft.AnalysisServices.DataSource> 的執行個體，才能加入新的 <xref:Microsoft.AnalysisServices.Dimension> 或 <xref:Microsoft.AnalysisServices.MiningStructure>。  
  
 ![AMO 類別高層級檢視](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-highlevelview-majorobjectshighlighted.gif "AMO 類別高層級檢視")  
  
 A*主要物件*是類別，表示完整的物件，為整個實體，而不要做為另一個物件的一部分。 主要物件包括 <xref:Microsoft.AnalysisServices.Server>、<xref:Microsoft.AnalysisServices.Cube>、<xref:Microsoft.AnalysisServices.Dimension> 和 <xref:Microsoft.AnalysisServices.MiningStructure>，因為這些是獨立的實體。 不過，<xref:Microsoft.AnalysisServices.Level> 不是主要物件，因為它是 <xref:Microsoft.AnalysisServices.Dimension> 的構成部分。 主要物件可以獨立於其他物件之外予以建立、刪除、修改或是處理。 次要物件是只能在建立父主要物件的過程中建立的物件。 次要物件通常會在主要物件建立時建立。 次要物件的值應該在建立時定義，因為預設不會建立次要物件。  
  
 下圖顯示 <xref:Microsoft.AnalysisServices.Server> 物件包含的主要物件。  
  
 ![反白顯示的 AMO 主要物件](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-majorobjects.gif "反白顯示的 AMO 主要物件")  
  
 ![反白顯示 AMO 主要物件 (2)](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-majorobjects-02.gif "反白顯示 AMO 主要物件 (2)")  
  
 當使用 AMO 設計程式時，類別與所含類別之間的關聯會使用集合類型屬性，例如 <xref:Microsoft.AnalysisServices.Server> 和 <xref:Microsoft.AnalysisServices.Dimension>。 若要使用所含類別的一個執行個體，必須先取得保存或是可保存所含類別的集合物件參考。 下一步，您在集合中尋找特定物件，然後您可以取得物件的參考，以便開始使用它。  
  
### <a name="amo-classes"></a>AMO 類別  
 AMO 是一個類別庫，用以從用戶端應用程式管理 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的執行個體。 AMO 類別庫可視為用以完成特定工作之物件的邏輯相關群組。 AMO 類別可用下列方式來分類：  
  
|類別集|目的|  
|---------------|-------------|  
|[AMO 基礎類別](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md)|必須有這些類別才能使用其他的類別集。|  
|[AMO OLAP 類別](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-olap-classes.md)|這些類別可讓您管理 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中的 OLAP 物件。|  
|[AMO 資料採礦類別](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-data-mining-classes.md)|這些類別可讓您管理 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中的資料採礦物件。|  
|[AMO 安全性類別](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-security-classes.md)|這些類別可讓您控制對其他物件的存取並維護安全性。|  
|[AMO 其他類別和方法](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-other-classes-and-methods.md)|協助 OLAP 或資料採礦管理員完成其每日工作的類別與方法。|  
  
##  <a name="bkmk_UsingAMO"></a>使用 AMO  
 AMO 對於自動化重複工作特別有用，例如根據事實資料表中的新資料，在量值群組中建立新資料分割，或是根據新資料重新定型採礦模型。 這些建立新物件的工作通常是每個月、每週或每季執行，而且應用程式可以根據新資料輕鬆地命名新物件。  
  
##### <a name="analysis-services-administrators"></a>Analysis Services 管理員  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 管理員可以使用 AMO 以自動化 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫的處理。 對於設計和部署 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫，您應該使用 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]。  
  
##### <a name="developers"></a>開發人員  
 開發人員可以使用 AMO 來為特定的使用者集合，開發管理介面。 這些介面可以限制對 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 物件的存取並限制使用者可執行的工作。 例如，透過使用 AMO，您可以建立備份應用程式，讓使用者可查看所有的資料庫物件，選取任何一個資料庫，並將它備份到一組指定裝置中的任何一個。  
  
 開發人員也可以在他們的應用程式中內嵌 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 邏輯。 基於此，開發人員可以根據使用者輸入或是其他因素，來建立 Cube、維度、採礦結構以及採礦模型。  
  
##### <a name="olap-advanced-users"></a>OLAP 進階使用者  
 OLAP 進階使用者通常是資料分析師或是其他有經驗的資料使用者，他們具有很強的程式設計背景，而且想要透過資料物件更周密的用法，來增強其資料分析。 對於需要離線工作的使用者而言，在離線之前使用 AMO 來自動化建立本機 Cube，將非常有用。  
  
##### <a name="data-mining-advanced-users"></a>資料採礦進階使用者  
 對於資料採礦的進階使用者而言，如果您有必須定期重新訓練的大量模型，AMO 會是最為實用的選擇。  
  
##  <a name="AutomatingAdministrativeTaskswithAMO"></a>使用 AMO 自動化管理工作  
 大部分重複性的工作如果是使用 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 來開發，會比開發成以任何所選語言撰寫的應用程式，更能妥善地設計、部署和維護。 不過，對於無法使用 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 來自動化的重複性工作，您可以使用 AMO。 當您想要使用 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 開發專業的商業智慧應用程式時，AMO 也會非常有用。  
  
##### <a name="automatic-object-management"></a>自動物件管理  
 透過 AMO，就可以根據使用者輸入或是新取得的資料，很輕鬆地建立、更新或是刪除 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 物件 (例如 <xref:Microsoft.AnalysisServices.Database>、<xref:Microsoft.AnalysisServices.Dimension>、<xref:Microsoft.AnalysisServices.Cube>、採礦 <xref:Microsoft.AnalysisServices.MiningStructure> 和 <xref:Microsoft.AnalysisServices.MiningModel>，或是 <xref:Microsoft.AnalysisServices.Role>)。 AMO 最適合用於必須從獨立軟體廠商，將已開發的方案部署到最終客戶的安裝應用程式。 安裝應用程式可以驗證是否有舊版存在，而且可以更新結構、移除不再有用的物件，並建立新的物件。 如果沒有舊版存在，則可以從頭建立所有的項目。  
  
 AMO 在根據新資料建立新資料分割方面非常強大，而且可以移除超過專案範圍的舊資料分割。 例如，對於處理過去 36 個月資料的財務分析方案，只要一收到新月份的資料，就可以移除第 37 個月的資料。 若要最佳化效能，可以根據使用方式設計新彙總並套用至過去 12 個月。  
  
##### <a name="automatic-object-processing"></a>自動物件處理  
 物件處理和更新的可用性可以透過使用 AMO 來達成，以回應超過一般流程資料以及使用 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 的排程工作的某些事件。  
  
##### <a name="automatic-security-management"></a>自動安全性管理  
 安全性管理可以自動化以便將新使用者加入角色及權限，或是在其他使用者的時間過期時予以移除。 您可以建立新介面以簡化安全管理員的安全性管理。 這會比使用 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 要更簡單。  
  
##### <a name="automatic-backup-management"></a>自動備份管理  
 透過使用 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 工作，或是透過建立會自動執行的專業 AMO 應用程式，就可以完成自動備份管理。 透過使用 AMO，您可以為操作員開發備份介面，以協助他們處理每日的作業。  
  
##### <a name="tasks-amo-is-not-intended-for"></a>不適合應用 AMO 的工作  
 AMO 無法用於查詢資料。 若要查詢 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料，包括 Cube 和採礦模型，請從使用者應用程式使用 ADOMD.NET。 如需詳細資訊，請參閱[使用 ADOMD.NET 來開發](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)。  
  
  
