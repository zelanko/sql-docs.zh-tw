---
title: "授與 Analysis Services 執行個體伺服器系統管理員權限 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- administrator rights [Analysis Services]
- server-wide administrative permissions [Analysis Services]
ms.assetid: 20d1234b-a457-4a84-ae08-fe356870c466
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 9caf9a17a4513c6261cad876ffb7aadce1c8ff09
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="grant-server-admin-rights-to-an--analysis-services-instance"></a>將伺服器系統管理員權限授與 Analysis Services 執行個體
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體內伺服器管理員角色的成員對於該執行個體中的所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件和資料具有不受限制的存取權。 使用者必須是伺服器管理員角色的成員，才能執行整個伺服器範圍的工作，例如建立資料庫或處理資料庫、修改伺服器屬性或啟動追蹤 (但處理事件不算)。  
  
 在安裝 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 時，會建立角色成員資格。 執行安裝程式的使用者可以將自己新增至角色，或新增其他使用者。 您必須先指定至少一位系統管理員，安裝程式才可讓您繼續進行。  
  
 依預設，也會將 Analysis Server 的管理權限授與本機 Administrators 群組的成員。 雖然本機群組未明確授與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器管理員角色的成員資格，但本機管理員可以建立資料庫，新增使用者和權限，以及執行系統管理員可執行的其他工作。 您可以設定隱含授與系統管理員權限。 它是由 **BuiltinAdminsAreServerAdmins** 伺服器屬性所決定，預設為 **true** 。 您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中變更這個屬性。 如需詳細資訊，請參閱 [Security Properties](../../analysis-services/server-properties/security-properties.md)。  
  
 安裝後，您可以修改角色成員資格來新增需要服務完整權限的任何其他使用者。 您也可以使用分析管理物件 (AMO) 來管理伺服器角色。 如需詳細資訊，請參閱[使用分析管理物件 &#40;AMO&#41; 來開發](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供在伺服器、資料庫和物件層級進行處理和查詢的逐漸細微角色的進度。 如需如何使用這些角色的指示，請參閱[角色與權限 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md)。  
  
## <a name="modify-server-role-membership"></a>修改伺服器角色成員資格  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體，然後以滑鼠右鍵按一下物件總管中的執行個體名稱，再按一下 [屬性]。  
  
2.  按一下 **[選取頁面]** 窗格中的 **[安全性]** ，然後按一下頁面底部的 **[加入]** ，以將一個或多個 Windows 使用者或群組加入至伺服器角色。  
  
     ![新增使用者對話方塊，在 management studio](../../analysis-services/instances/media/ssas-serveradminadd.png "新增在 management studio [使用者] 對話方塊")  
  
### <a name="add-computer-accounts"></a>新增電腦帳戶  
 您也可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 將電腦帳戶設為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Administrators 群組的成員。  
  
1.  在 [選取使用者或群組]  對話方塊中，按一下 [位置] 。  
  
2.  選取您想要新增之電腦所屬的網域，或選取 [整個目錄]  ，然後按一下 [確定] 。  
  
3.  按一下 **[物件類型]**。  
  
4.  選取 [電腦]  ，然後按一下 [確定] 。  
  
     ![將電腦帳戶新增為 ssas 管理員](../../analysis-services/instances/media/ssas-in-ssms-computerobjects.png "ssas 系統管理員的身分新增電腦帳戶")  
  
5.  在 [輸入要選取的物件名稱]  文字方塊中，輸入電腦的名稱，然後按一下 [檢查名稱]  確認電腦帳戶位於目前的位置。 如果找不到電腦帳戶，請確認電腦名稱以及電腦所屬的網域正確。  
  
## <a name="nt-servicessastelemetry-account"></a>NT Service\SSASTelemetry 帳戶  
 **NT Service/SSASTelemetry** 是在安裝期間建立的低權限電腦帳戶，且專用來執行客戶經驗改進計畫 (CEIP) 服務的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 實作。 此服務需要有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的系統管理員權限，才能執行數個探索命令。 如需詳細資訊，請參閱＜ [Customer Experience Improvement Program for SQL Server Data Tools](../../sql-server/customer-experience-improvement-program-for-sql-server-data-tools.md) ＞和＜ [Microsoft SQL Server Privacy Statement](http://msdn.microsoft.com/library/57769f4a-5689-49a1-8298-e3c0db5106f8) ＞。  
  
## <a name="see-also"></a>另請參閱  
 [物件和作業的存取權授權 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)   
 [安全性角色 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)  
  
  
