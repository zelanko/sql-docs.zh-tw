---
title: "安全性概觀 （資料採礦） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [Analysis Services - data mining], about security
ms.assetid: 387bde00-bcf3-4612-b27b-f9f608dbf71e
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4857608190aa03baca0a6916275641f463c6cf2a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="security-overview-data-mining"></a>安全性概觀 (資料採礦)
  保護 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 之安全的程序發生在多個層級上。 您必須保護 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的每一個執行個體及其資料來源的安全，以確定只有獲得授權的使用者對於選取的維度、採礦模型和資料來源，具有讀取或讀取/寫入權限。 您也必須保護基礎資料來源的安全，以防止未經授權的使用者惡意破壞機密商業資訊。 下列主題描述保護 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體之安全的程序。  
  
##  <a name="bkmk_Architecture"></a> 安全性架構  
 請參閱以下資源，以了解 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體的基本安全性架構，包括 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 如何使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 驗證來驗證使用者存取權。  
  
-   [安全性角色 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)  
  
-   [安全性屬性](../../analysis-services/server-properties/security-properties.md)  
  
-   [設定服務帳戶 &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md)  
  
-   [物件和作業的存取權授權 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
##  <a name="bkmk_Logon"></a> 設定 Analysis Services 的登入帳戶  
 您必須為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 選取適當的登入帳戶，並指定此帳戶的權限。 您必須確定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 登入帳戶只具有執行必要工作所必須的權限，包括基礎資料來源的適當權限。  
  
 若是資料採礦，您需要一組與檢視或查詢模型所需的不同權限來建立與處理模型。 根據模型進行預測是一種查詢，而且不需要管理權限。  
  
##  <a name="bkmk_Instance"></a> 保護 Analysis Services 執行個體的安全  
 接下來，您必須保護 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 電腦、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 電腦上的 Windows 作業系統、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 本身以及 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用的資料來源等項目的安全。  
  
##  <a name="bkmk_Access"></a> 設定 Analysis Services 的存取權  
 當您設定和定義 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體的授權使用者時，需要決定哪些使用者也應具有權限來管理特定資料庫物件、哪些使用者可以檢視物件的定義或瀏覽模型，以及哪些使用者可以直接存取資料來源。  
  
##  <a name="bkmk_DMspecial"></a> 資料採礦的特殊考量  
 若要讓分析師或開發人員建立及測試資料採礦模型，您必須提供該分析師或開發人員儲存採礦模型所在之資料庫的管理權限。 因此，資料採礦分析師或開發人員可能可以建立或刪除與資料採礦不相關的其他物件，包括其他分析師或開發人員建立並使用的資料採礦物件，或不包含在資料採礦方案中的 OLAP 物件。  
  
 同時，當您建立資料採礦的方案時，必須根據其他使用者的需求，平衡分析師或開發人員開發、測試與微調模型的需求，並採取保護現有資料庫物件的措施。 其中一種可能的方法是建立資料採礦專用的另一個資料庫，或針對每個分析師建立個別的資料庫。  
  
 雖然建立模型需要最高層級的權限，但是您可以使用以角色為基礎的安全性，控制使用者對於資料採礦模型的存取權以進行其他作業，例如，處理、瀏覽或查詢。 當您建立角色時，會設定資料採礦物件專屬的權限。 身為角色成員的任何使用者都會自動擁有與該角色相關聯的所有權限。  
  
 此外，資料採礦模型通常會參考包含敏感資訊的資料來源。 如果採礦結構與採礦模型已經設定為允許使用者從模型鑽研到結構中的資料，您必須採取預防措施，為機密資訊進行遮罩，或限制可以存取基礎資料的使用者。  
  
 如果您使用 Integration Services 封裝清除資料、更新採礦模型或進行預測，您必須確保 Integration Services 服務具備儲存模型所在之資料庫的適當權限，以及來源資料的適當權限。  
  
## <a name="see-also"></a>請參閱＜  
 [角色與權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md)  
  
  

