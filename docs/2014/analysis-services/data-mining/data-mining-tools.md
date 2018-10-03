---
title: 資料採礦工具 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- tools [Analysis Services]
- mining models [Analysis Services], tools
- data mining [Analysis Services], tools
- data mining [Analysis Services], development
ms.assetid: 003ada6a-0bcd-4f16-8c34-1a9ffc75cd2c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 70669026a7953ba1c2818ebc35b3d8fa7cb55427
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171548"
---
# <a name="data-mining-tools"></a>資料採礦工具。
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會提供您可用來建立資料採礦方案的以下工具：  
  
-    中的資料採礦精靈 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 可讓您在 Cube 中使用關聯式資料來源或多維度資料，輕鬆建立採礦結構和採礦模型。  
  
     在此精靈中，您會選擇要使用的資料，然後套用特定的資料採礦技術，例如叢集、類神經網路或時間序列模型。  
  
-    和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中都有提供模型檢視器 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，可讓您在建立採礦模型之後加以探索。  您可以使用針對每一個演算法所量身打造的檢視器來瀏覽模型，或者可以使用模型內容檢視器深入分析。  
  
-    和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中都有提供預測查詢產生器 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ，可幫助您建立預測查詢。 您也可以針對鑑效組資料集或外部資料來測試模型的精確度，或者使用交叉驗證來評估資料集的品質。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 是您用來管理現有資料採礦方案的介面，這些方案已經部署到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的執行個體。 您可以重新處理結構和模型，以更新其中的資料。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含一些工具，您可使用這些工具來清除資料、自動化工作 (例如建立預測和更新模型) 及建立文字採礦方案。  
  
 下列章節提供有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中之資料採礦工具的詳細資訊。  
  
## <a name="data-mining-wizard"></a>資料採礦精靈  
 使用資料採礦精靈開始建立資料採礦方案。 此精靈非常快速且容易使用，可引導您建立資料採礦結構和初始相關之採礦模型的程序，並包含選取演算法類型和資料來源以及定義案例資料進行分析的工作。  
  
 **如需詳細資訊︰**[Data Mining Wizard &#40;Analysis Services - Data Mining&#41;](data-mining-wizard-analysis-services-data-mining.md) (資料採礦精靈 (Analysis Services - 資料採礦))。  
  
## <a name="data-mining-designer"></a>[資料採礦設計師]  
 在您使用資料採礦精靈建立採礦結構和採礦模型之後，您可以從 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 使用資料採礦設計師來處理現有的模型與結構。  
  
 此設計師包含適用於以下工作的工具：  
  
-   修改採礦結構的屬性、加入資料行及建立資料行別名、變更分類收納方法或預期的值分佈。  
  
-   將新的模型加入現有的結構中；複製模型、變更模型屬性或中繼資料，或是定義採礦模型的篩選。  
  
-   瀏覽模型中的模式與規則；探索關聯或決策樹。 取得詳細統計資料  
  
     每一個不同的時間序列模型都會提供自訂檢視器，幫助您分析資料及探索資料採礦所揭露的模式。  
  
-   藉由建立增益圖或分析模型的收益曲線來驗證模型。 使用分類矩陣比較模型，或是使用交叉驗證來驗證資料集及其模型。  
  
-   針對現有的採礦模型建立預測和內容查詢。 建立一次性查詢，或是設定查詢來針對外部資料的整個資料表產生預測。  
  
 **如需詳細資訊：** [資料採礦設計師](data-mining-designer.md)  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 在您建立並將採礦模型部署到伺服器之後，您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來管理裝載資料採礦物件的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。 您也可以繼續執行使用此模型的工作，例如瀏覽模型、處理新的資料和建立預測。  
  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 也包含查詢編輯器，您可以用來設計及執行資料採礦延伸 (DMX) 查詢，或是透過 XMLA 來處理資料採礦物件。  
  
## <a name="integration-services-data-mining-tasks-and-transformations"></a>Integration Services 資料採礦工作和轉換  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供了許多支援資料採礦的元件。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的一些工具的目的是為了將常見的資料採礦工作自動化，包括預測、模型建立和處理。 例如：  
  
-   建立 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，每當新的客戶更新資料集時，此封裝都會自動更新模型  
  
-   執行案例記錄的自訂分割或自訂取樣。  
  
-   根據傳遞的參數自動產生模型。  
  
 但是，您也可以在封裝工作流程中使用資料採礦當做其他處理序的輸入。 例如：  
  
-   使用模型產生的機率值，針對文字採礦或其他分類工作的分數來加權。  
  
-   根據之前的資料自動產生預測，並使用這些值來評估新的值的有效性。  
  
-   使用羅吉斯迴歸，根據風險區隔送入的客戶。  
  
 **如需詳細資訊：**[Related Projects for Data Mining Solutions](data-mining-solutions.md) (資料採礦方案的相關專案)  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組&#40;DMX&#41;參考](/sql/dmx/data-mining-extensions-dmx-reference)   
 [採礦模型工作和使用說明](mining-model-tasks-and-how-tos.md)   
 [採礦模型檢視器工作和使用說明](mining-model-viewer-tasks-and-how-tos.md)   
 [資料採礦方案](data-mining-solutions.md)  
  
  
