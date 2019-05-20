---
title: 在原生模式報表伺服器上授與權限 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- roles [Reporting Services], creating
- authorization [Reporting Services]
- server security [Reporting Services]
- role-based security [Reporting Services]
- items [Reporting Services], security
- permissions [Reporting Services], native mode
- published reports [Reporting Services], security
- reports [Reporting Services], security
- report items [Reporting Services], security
- role-based security [Reporting Services], about role-based security
- security [Reporting Services], role-based
ms.assetid: 260dc2e9-546c-4f04-9fa1-977e23c9d68c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d38bcdb965bc08aa4eb7cad1401bd9d77f42b4ed
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2019
ms.locfileid: "65579828"
---
# <a name="granting-permissions-on-a-native-mode-report-server"></a>在原生模式報表伺服器上授與權限
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會使用以角色為基礎的授權和驗證子系統來決定能夠在報表伺服器上執行作業及存取項目的人員。 以角色為基礎的授權，將使用者或群組可以執行的動作集分類成角色。 驗證是以內建的 Windows 驗證或您提供的自訂驗證模組為基礎。 您可以使用預先定義或自訂的角色搭配任何一種驗證類型。  
  
## <a name="using-roles-to-grant-report-server-access"></a>使用角色來授與報表伺服器存取權  
 所有使用者都會在定義特定存取層級的角色內容中與報表伺服器進行互動。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包含了一些預先定義的角色，而且您可以將這些角色指派給使用者和群組，以便提供報表伺服器的立即存取權。 **ContentManager**、 **Publisher**和 **Browser** 是預先定義角色的範例。 每個角色都會定義相關工作的集合。 例如， **發行者** 擁有加入報表以及建立儲存這些報表之資料夾的權限。  
  
 雖然角色指派通常是從父節點所繼承的，但是您也可以透過針對特定項目建立新的角色指派，中斷權限繼承。 屬於某份報表之 **內容管理員** 角色成員的使用者可能是另一份報表之 **瀏覽者** 角色的成員。  
  
 若要授與報表伺服器項目和作業的存取權，請遵循下列指導方針：  
  
1.  檢閱預先定義的角色來判斷您是否能夠依原狀使用它們。 如果您需要調整工作或定義其他角色，就應該先進行這些作業，然後再指派使用者至特定角色。 如需各個角色的詳細資訊，請參閱 [Predefined Roles](../../reporting-services/security/role-definitions-predefined-roles.md)。  
  
2.  確認哪些使用者和群組需要存取報表伺服器，以及所存取的層級。 多數使用者都應指派至 **[瀏覽者]** 角色或 **[報表產生器]** 角色。 **[發行者]** 角色則應指派給較少數的使用者。 只有非常少數的使用者才應指派至 **[內容管理員]**。  
  
3.  您可以使用報表管理員，針對需要存取權的每個使用者或群組，指派 [主資料夾] 資料夾 (這是報表伺服器資料夾階層的最上層資料夾) 的角色。  
  
4.  在網站層級，於報表管理員的 [網站設定] 頁面上，使用 **系統使用者** 和 **系統管理員**等預先定義的角色，為每個使用者或群組建立系統層級角色指派。  
  
5.  視需要針對特定資料夾、報表和其他項目建立其他角色指派。 請避免建立大量角色指派。 如果您建立過多角色指派，可能會難以針對每個使用者追蹤不同的權限層級。  
  
> [!NOTE]  
>  如果您設定報表伺服器在 SharePoint 整合模式中執行，您必須在 SharePoint 網站上設定權限，授與報表伺服器項目的存取權。 如需詳細資訊，請參閱 [授與 SharePoint 網站上報表伺服器項目的權限](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)。  
  
## <a name="who-sets-permissions"></a>誰設定權限  
 一開始，只有屬於本機管理員群組成員的使用者可以存取報表伺服器。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 已安裝二個預設角色指派，其將項目層級及系統層級的存取權授與本機管理員群組的成員。 這些內建角色指派會將報表伺服器存取權授與其他使用者並管理報表伺服器項目。 您無法刪除內建的角色指派。 本機管理員一律擁有完全管理報表伺服器執行個體的權限。  
  
 由於報表伺服器的完整權限包括項目層級和系統層級的權限，因此本機管理員會被指派至下列角色：  
  
 您必須進行其他組態設定，然後才能管理執行 Windows Vista 或 Windows Server 2008 之本機電腦上的報表伺服器執行個體。 如需詳細資訊，請參閱 [設定原生模式報表伺服器進行本機管理 &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
## <a name="how-permissions-are-stored"></a>權限的儲存方式  
 角色指派和定義會儲存在報表伺服器資料庫中。 如果您要使用各種用戶端工具或程式設計介面，所有存取方式都會受限於針對整個報表伺服器執行個體定義的權限。 如果您在向外延展部署中設定多部報表伺服器，那麼在其中一個執行個體上定義的角色指派會儲存在共用資料庫中，提供給相同向外延展部署中的所有其他執行個體使用。 由於角色指派會與它們保護的項目一起儲存，因此您可以將資料庫移至其他報表伺服器執行個體，而不會遺失您所定義的權限。  
  
## <a name="tasks-and-tools-for-managing-permissions"></a>管理權限的工作和工具  
 您可以使用下列工具來管理角色定義和指派。  
  
|工具|工作|  
|----------|-----------|  
|Management Studio - 用於檢視、修改、建立和刪除角色定義。|[建立、刪除或修改角色 &#40;Management Studio&#41;](../../reporting-services/security/role-definitions-create-delete-or-modify.md)|  
|報表管理員 - 用於指派使用者和群組給角色。|[將報表伺服器的存取權授與使用者 &#40;報表管理員&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md)<br /><br /> [修改或刪除角色指派 &#40;報表管理員&#41;](../../reporting-services/security/role-assignments-modify-or-delete.md)|  
  
## <a name="see-also"></a>另請參閱  
 [Predefined Roles](../../reporting-services/security/role-definitions-predefined-roles.md)   
 [授與 SharePoint 網站上報表伺服器項目的權限](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [使用報表伺服器驗證](../../reporting-services/security/authentication-with-the-report-server.md)   
 [建立和管理角色指派](../../reporting-services/security/create-and-manage-role-assignments.md)   
 [Reporting Services 安全性與保護](../../reporting-services/security/reporting-services-security-and-protection.md)   
 [報表伺服器內容管理 &#40;SSRS 原生模式&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)  
  
  
