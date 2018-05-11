---
title: 連結量值群組 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3414f54c9212679c4dd29192caa3e6fd57c70bb9
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="linked-measure-groups"></a>連結量值群組
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  連結的量值群組會以相同資料庫或不同的 Analysis Services 資料庫中不同之 Cube 中的另一個量值群組為基礎。 如果您想要重複使用多個 Cube 中的一組量值及對應的資料值，您可使用連結量值群組。  
  
 Microsoft 建議原始和連結的量值群組皆位於同一部伺服器上所執行的解決方案中。 連結到遠端伺服器上的量值群組已排定從未來的版本中淘汰 (請參閱 [SQL Server 2016 中已被取代的 Analysis Services 功能](../../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md))。  
  
> [!IMPORTANT]  
>  連結量值群組是唯讀的。 若要挑選最新的變更，您必須先刪除所有連結量值群組，再根據修改的來源物件重新建立連結量值群組。 基於這個理由，未來需要修改量值群組時，建議您考慮在專案之間複製並貼上量值群組這個替代方法。  
  
## <a name="usage-limitations"></a>使用方式的限制  
 如同先前所註明，使用連結量值的一個重要限制就是無法直接自訂連結量值。 修改資料類型、格式、資料繫結和可見度以及量值群組本身之項目的成員資格是原始量值群組中所必須進行的所有變更。  
  
 就作業上而言，透過用戶端應用程式進行存取時，連結量值群組與其他量值群組相同，而查詢方式也與其他量值群組相同。  
  
 查詢含有連結量值群組的 Cube 時，會在目的地 Cube 的第一次計算行程中，建立和解析連結。 因為這樣的行為，所以在評估查詢之前，無法解析儲存在連結量值群組中的任何計算。 換句話說，必須在目的地 Cube 中重新建立導出量值和導出資料格，而不是從來源 Cube 繼承而來。  
  
 下列清單摘要說明使用上的限制。  
  
-   您不可從另一個連結量值群組建立連結量值群組。  
  
-   您不可在連結量值群組中加入或移除量值。 成員資格只會定義在原始量值群組中。  
  
-   連結量值群組不支援回寫。  
  
-   連結量值群組無法用於多個多對多關聯性，特別是當這些關聯性位於不同 Cube 時。 這樣做可能會導致模糊不清的彙總。 如需詳細資訊，請參閱 [包含多對多關聯性之 Cube 中連結量值的數量不正確](http://social.technet.microsoft.com/wiki/contents/articles/22911.incorrect-amounts-for-linked-measures-in-cubes-containing-many-to-many-relationships-ssas-troubleshooting.aspx)。  
  
 連結量值群組中所包含的量值，只能和從同一個 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫擷取的連結維度直接進行組織。 但是，您可以使用導出成員，將連結量值群組的資訊與您 Cube 中其他非連結維度產生關聯。 您也可以使用間接關聯性，例如參考或多對多關聯性，將非連結維度與連結量值群組產生關聯。  
  
## <a name="create-or-modify-a-linked-measure"></a>建立或修改連結量值  
 使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 建立連結量值群組。  
  
1.  現在完成來源 Cube 中原始量值群組的任何修改，這樣您稍後就不必在後續的 Cube 中重建連結量值群組。 您可以重新命名連結物件，但是不得變更其他任何屬性。  
  
2.  在 [方案總管] 中，按兩下要將連結量值群組加入至哪一個 Cube。 這個步驟會在 Cube 設計師中開啟 Cube。  
  
3.  在 Cube 設計師的 [量值] 窗格或 [維度] 窗格中，以滑鼠右鍵按一下其中一個窗格的任何地方，然後選取 [新增連結物件]。 這樣會啟動連結物件精靈。  
  
4.  在第一個頁面上，指定資料來源。 這個步驟會建立原始量值群組的位置。 預設值為目前資料庫中現有的 Cube，但是您也可以選擇不同的 Analysis Services 資料庫。  
  
5.  在下一頁選擇您想要連結的量值群組或維度。 維度和 Cube 物件 (例如量值群組) 會個別列出。 只有尚未在目前 Cube 中的物件才可使用。  
  
6.  按一下 [完成] 即可建立連結物件。 連結物件會出現在 [量值和維度] 窗格中 (以連結圖示指示)。  
  
## <a name="secure-a-linked-measure"></a>維護連結量值的安全  
 定義連結之後，管理連結量值群組中量值的存取權方式，就和管理其他量值群組存取權的方式一樣。 連結物件會連同其非連結的對應項目一起出現在角色設計工具中。 如需管理量值群組之安全性的詳細資訊，請參閱[授與 Cube 或模型權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)。  
  
 若要定義或使用連結量值群組，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的 Windows 服務帳戶必須屬於 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫角色 (而此角色擁有來源 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上對來源 Cube 和量值群組的 **ReadDefinition** 和 **Read** 存取權限)，或必須屬於來源 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理員角色。  
  
## <a name="see-also"></a>另請參閱  
 [定義連結維度](../../analysis-services/multidimensional-models/define-linked-dimensions.md)  
  
  
