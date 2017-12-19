---
title: "授與資料庫權限 (Analysis Services) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permissions [Analysis Services], full control
- full control permissions [Analysis Services]
ms.assetid: be7e5f64-af43-47d6-84a5-c5c1c277d644
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: d313637275d28a83b8a0f79e23bfc46bd972ae2a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="grant-database-permissions-analysis-services"></a>授與資料庫權限 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]處理 Analysis Services 資料庫管理與在關聯式資料庫背景時，如果您需要了解第一件事是，根據資料存取的資料庫不是 Analysis Services 中的主要安全性實體物件。  
  
 Analysis Services 中主要的查詢結構是 Cube (或表格式模型)，以及在這些特定物件上設定的使用者權限。 對照關聯式資料庫引擎 (已在資料庫本身設定資料庫登入和使用者權限 (通常是 **db_datareader**)，Analysis Services 資料庫大部分都是資料模型中主要查詢物件的容器。 如果您當前的目標是針對 Cube 或表格式模型啟用資料存取，您可以立即略過資料庫權限，並直接前往以下主題：[授與 Cube 或模型權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)。  
  
 Analysis Services 中的資料庫權限可以啟用管理功能；廣泛來說，就是使用 [完整控制權] 資料庫權限的情況，或者，如果您正在委派處理作業，就是更細微的類別。 Analysis Services 資料庫的權限等級是在 [建立角色] 對話方塊的 [一般] 窗格中指定，如下圖所示且如下所述。  
  
 Analysis Services 中不需任何登入。 您只需建立角色，並在 [成員資格] 窗格中指派 Windows 帳戶即可。 包含管理員在內的所有使用者都是使用 Windows 帳戶連線到 Analysis Services。  
  
 ![建立角色 對話方塊顯示資料庫的權限](../../analysis-services/multidimensional-models/media/ssas-permsdbrole.png "建立角色 對話方塊顯示資料庫的權限")  
  
 有三種權限類型是在資料庫層級指定。  
  
 **完整控制權 (管理員)** - [完整控制權] 是全包型權限，在 Analysis Services 資料庫上具備強大的控制能力，例如，能夠查詢或處理資料庫內的任何物件，以及管理角色安全性。 [完整控制權] 相當於資料庫管理員狀態。 當您選取 [完整控制權] 時，也會同時選取 [處理資料庫] 和 [讀取定義] 權限且無法移除。  
  
> [!NOTE]  
>  伺服器管理員 (伺服器管理員角色的成員) 也會在伺服器中的每個資料庫上擁有隱含的完整控制權。  
  
 **處理資料庫** - 這個權限是用來在資料庫層級委派處理。 身為管理員，您可以透過建立允許其他人員或服務為資料庫中任何物件叫用處理作業的角色，來將此工作交由其他人執行。 或者，您也可以建立在特定物件上啟用處理的角色。 如需詳細資訊，請參閱 [授與處理權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md) 。  
  
 **讀取定義** - 這個權限會授與讀取物件中繼資料的能力，但不包括檢視相關資料的能力。 通常，這個權限是在針對專屬處理所建立的角色中使用，新增這個能力之後即可使用像是 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 這樣的工具，來以互動方式處理資料庫。 在沒有 [讀取定義] 的情況下，[處理資料庫] 權限只有在已編寫指令碼的情況下才有效。 如果您規劃自動處理 (可能是透過 SSIS 或其他排程器)，您可能想要建立擁有 [處理資料庫] 但沒有 [讀取定義] 的角色。 除此之外，請考量在相同角色中將這兩個屬性結合在一起，以透過 SQL Server 工具支援自動和互動式處理，這類工具可將使用者介面中的資料模型視覺化。  
  
## <a name="full-control-administrator-permissions"></a>完整控制權 (管理員) 權限  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，資料庫管理員是任何已指派給包含完整控制權 (管理員) 權限之角色的 Windows 使用者識別。 資料庫管理員可以執行資料庫內的任何工作，包含：  
  
-   處理物件  
  
-   讀取資料庫中所有物件的資料和中繼資料，包含 Cube、維度、量值群組、檢視方塊及資料採礦模型  
  
-   藉由新增使用者或權限來建立或修改資料庫角色，包括將使用者新增到也擁有 [完整控制權] 權限的角色  
  
-   刪除資料庫角色或角色成員資格  
  
-   註冊資料庫的組件 (或預存程序)。  
  
 請注意，資料庫管理員無法在伺服器上新增或刪除資料庫，或將管理員權限授與同一部伺服器上的其他資料庫。 這個權限僅屬於伺服器管理員。 如需此權限等級的詳細資訊，請參閱 [將伺服器管理員權限授與 Analysis Services 執行個體](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md) 。  
  
 因為所有角色都是使用者定義的，所以，建議您建立專門用於此用途的角色 (例如，名為 "dbadmin" 的角色)，然後據以指派 Windows 使用者和群組帳戶。  
  
#### <a name="create-roles-in-ssms"></a>在 SSMS 中建立角色  
  
1.  在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，連接到的執行個體[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，開啟**資料庫**資料夾中，選取資料庫，並以滑鼠右鍵按一下**角色** | **新角色**.  
  
2.  在 [一般] 窗格中，輸入名稱，例如 DBAdmin。  
  
3.  選取 Cube 的 [完整控制權 (管理員)] 核取方塊。 請注意，系統會自動選取 [處理資料庫] 和 [讀取定義]。 這兩個權限一律會包含在包括 [完整控制權] 的角色中。  
  
4.  在 [成員資格] 窗格中，輸入使用這個角色連接到 Analysis Services 的 Windows 使用者和群組帳戶。  
  
5.  按一下 [確定]，完成角色的建立。  
  
## <a name="process-database"></a>處理資料庫  
 定義授與資料庫權限的角色時，您可以略過 [完整控制權]，僅選擇 [處理資料庫]。 這個在資料庫層級設定的權限允許在資料庫內的所有物件上執行處理作業。 如需詳細資訊，請參閱 [授與處理權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)  
  
## <a name="read-definition"></a>讀取定義  
 就像 [處理資料庫] 一樣，在資料庫層級設定 [讀取定義] 權限也會對資料庫內的其他物件產生串聯效果。 如果您想要在更細微的層級上設定 [讀取定義] 權限，您必須清除在 [一般] 窗格中以資料庫屬性方式顯示的 [讀取定義]。 如需詳細資訊，請參閱[授與物件中繼資料的讀取定義權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md)。  
  
## <a name="see-also"></a>請參閱  
 [將伺服器管理員權限授與 Analysis Services 執行個體](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [授與處理權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)  
  
  
