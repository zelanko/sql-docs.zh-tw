---
title: "授與物件和作業 (Analysis Services) 存取權 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
f1_keywords:
- sql13.asvs.roledesignerdialog.general.f1
- sql13.asvs.roledesignerdialog.membership.f1
helpviewer_keywords:
- access rights [Analysis Services], users
- permissions [Analysis Services], users
- security [Analysis Services], user access
- user access rights [Analysis Services]
- granting permissions [Analysis Services], users
ms.assetid: af28524e-5eca-4dce-a050-da4f406ee1c7
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: cff9bdcefc19729ed8f29a1fe8f04267e03ddf4a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="authorizing-access-to-objects-and-operations-analysis-services"></a>物件和作業的存取權授權 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]非系統管理使用者存取 cube、 維度和採礦模型內[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫透過一或多個資料庫角色的成員資格授與。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 系統管理員可以建立這些資料庫角色、授與這些角色對 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的讀取或讀取/寫入權限，然後將 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 使用者和群組指派給每個角色。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會結合與使用者或群組所屬的每一個資料庫角色相關聯的權限，來決定特定 Windows 使用者或群組的有效權限。 因此，如果某個資料庫角色沒有授與使用者或群組檢視維度、量值或屬性的權限，但另一個資料庫角色有授與該使用者或群組該權限，則該使用者或群組將具有檢視該物件的權限。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器管理員角色的成員與具有完整控制權 (管理員) 權限之資料庫角色的成員，可以存取資料庫中的所有資料和中繼資料，不需其他權限就可以檢視特定物件。 而且， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器角色成員存取任何資料庫中的任何物件時都不能遭到拒絕，而在資料庫內具有完整控制權 (管理員) 權限的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫角色，存取該資料庫內的任何物件時也不能遭到拒絕。 特殊的系統管理作業 (例如處理) 可透過權限較少的個別角色來授權。 如需詳細資訊，請參閱[授與處理權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)。  
  
## <a name="list-roles-defined-for-your-database"></a>列出為您的資料庫定義的角色  
 系統管理員可以在 SQL Server Management Studio 中執行簡單的 DMV 查詢，以取得伺服器上定義的所有角色清單。  
  
1.  在 SSMS 中，以滑鼠右鍵按一下資料庫，然後選取**新查詢** | **MDX**。  
  
2.  輸入下列查詢並按 F5 來執行：  
  
    ```  
    Select * from $SYSTEM.DBSCHEMA_CATALOGS  
    ```  
  
     結果包含資料庫名稱、描述、角色名稱及上次修改日期。 使用此資訊做為起點，您可以對個別的資料庫繼續執行，以檢查特定角色的成員資格與權限。  
  
## <a name="top-down-overview-of-analysis-services-authorization"></a>由上而下的 Analysis Services 授權概觀  
 本節涵蓋設定權限的基本工作流程。  
  
 **步驟 1︰伺服器管理**  
  
 第一個步驟是決定誰具有伺服器層級的系統管理員權限。 在安裝期間，安裝 SQL Server 的本機管理員需要指定一或多個 Windows 帳戶做為 Analysis Services 伺服器管理員。 伺服器管理員擁有伺服器上所有可能的權限，包含檢視、修改及刪除伺服器上的任何物件，或檢視相關聯資料的權限。 安裝完成後，伺服器管理員可以新增或移除帳戶來變更這個角色的成員資格。 如需此權限等級的詳細資訊，請參閱 [將伺服器管理員權限授與 Analysis Services 執行個體](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md) 。  
  
 **步驟 2︰資料庫管理**  
  
 接著，在表格式或多維度方案建立後，就會將它部署到伺服器做為資料庫。 伺服器管理員可以透過為有問題的資料庫定義擁有完整控制權限的角色，來委派資料庫管理工作。 這個角色的成員可以處理或查詢資料庫中的物件，也可以建立其他角色來存取資料庫本身內的 Cube、維度和其他物件。 如需詳細資訊，請參閱[授與資料庫權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)。  
  
 **步驟 3︰啟用查詢和處理工作負載的 Cube 或模型存取權**  
  
 根據預設，只有伺服器和資料庫系統管理員可以存取 Cube 或表格式模型。 讓組織中的其他人員可以使用這些資料結構，需要其他角色指派來將 Windows 使用者和群組帳戶對應到 Cube 或模型，以及指定 [讀取] 權限 (Privilege) 的權限 (Permission)。 如需詳細資訊，請參閱[授與 Cube 或模型權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)。  
  
 處理工作可以和其他系統管理功能分開進行，因此，伺服器和資料庫系統管理員可將此工作委派給他人，或透過指定執行排程軟體的服務帳戶設定自動處理。 如需詳細資訊，請參閱[授與處理權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)。  
  
> [!NOTE]  
>  使用者不需要對 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 用於載入資料之基礎關聯式資料庫中的關聯式資料表具有任何權限，也不需要對執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 之執行個體的電腦具有任何檔案層級權限。  
  
 **步驟 4 (選擇性)︰允許或拒絕對內部 Cube 物件的存取**  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供在個別物件 (包括資料模型內的維度成員和資料格) 設定權限的安全性設定。 如需詳細資訊，請參閱[授與維度資料的自訂存取權 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) 和[授與資料格資料的自訂存取權 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)。  
  
 您也可以根據使用者識別來變動權限。 這通常稱為動態安全性，可以使用 [UserName &#40;MDX&#41;](../../mdx/username-mdx.md) 函數來實作  
  
## <a name="best-practices"></a>最佳做法  
 若要以更好的方式管理權限，建議使用如下的處理方式：  
  
1.  依功能建立角色 (例如，dbadmin、cubedeveloper、processadmin)，如此一來，無論是誰維護角色，都能一眼就看出該角色所允許執行的功能。 如同其他內容所述，您可以在模型定義中定義角色，因而能夠透過後續的解決方案部署來保留這些角色。  
  
2.  在 Active Directory 中建立相對應的 Windows 安全性群組，然後在 Active Directory 中維護該安全性群組，以確保它會包含適當的個別帳戶。 這讓組織中已經精通用於帳戶維護之工具和處理程序的安全性專業人員肩負安全性群組成員資格的責任。  
  
3.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中產生指令碼，如此一來，每當從模型的來源檔案將模型重新部署到伺服器時，您便能快速複寫角色指派。 如需如何快速產生指令碼的詳細資訊，請參閱[授與 Cube 或模型權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)。  
  
4.  採用可反映角色的範圍與成員資格的命名慣例。 只有在設計和系統管理工具中看得見角色名稱，因此，請使用讓 Cube 安全性專員可以理解的命名慣例。 例如， **processadmin-windowsgroup1** 表示要對組織中個別 Windows 使用者帳戶為 **windowsgroup1** 安全性群組成員的人員授與讀取存取權與處理權限。  
  
     包含帳戶資訊可協助您追蹤在各種不同角色中使用了哪些帳戶。 由於角色是加總的，因此與 **windowsgroup1** 相關聯的組合角色，能夠為隸屬於該安全性群組的人員組成有效的權限集。  
  
5.  Cube 開發人員需要開發中模型和資料庫的完整控制權限，但是一旦資料庫部署到實際執行伺服器後，便只需要讀取權限。 請記得為所有案例開發角色定義和指派項目，包括開發、測試及實際執行部署。  
  
 使用與此類似的方法能避免模型中的角色定義和角色成員資格紊亂，並為角色指派提供能見度，讓 Cube 權限在實作和維護上會更容易些。  
  
## <a name="see-also"></a>請參閱  
 [將伺服器管理員權限授與 Analysis Services 執行個體](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [角色與權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md)   
 [Analysis Services 支援的驗證方法](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)  
  
  
