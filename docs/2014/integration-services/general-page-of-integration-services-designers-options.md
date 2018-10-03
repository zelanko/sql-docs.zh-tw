---
title: 一般頁面 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Business_Intelligence_Designers.Data_Transformation_Designers.General
ms.assetid: d695690a-923b-4036-945e-7621e8651deb
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 16a62e70239db5688fc37b34f3b11752f43178d6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48151012"
---
# <a name="general-page"></a>一般頁面
  在 [選項] 對話方塊上使用 [Integration Services 設計師] 頁面上的 [一般] 頁面，指定用來載入、顯示及升級封裝的選項。  
  
 若要開啟 [一般] 頁面，請在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的 [工具] 功能表上按一下 [選項]，然後展開 [商業智慧設計師]，再選取 [Integration Services 設計師]。  
  
## <a name="options"></a>選項。  
 **載入封裝時檢查數位簽章**  
 選取即可讓 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 在載入封裝時檢查數位簽章。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 只會檢查數位簽章是否存在、是否有效，以及是否來自信任的來源。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 將不會檢查此封裝在簽署之後是否已經變更。  
  
 如果您設定 **BlockedSignatureStates** 登錄值，此登錄值會覆寫 [載入封裝時檢查數位簽章] 選項。 如需詳細資訊，請參閱[透過設定登錄值實作簽署原則](implement-a-signing-policy-by-setting-a-registry-value.md)。  
  
 如需詳細資訊，請參閱 [使用數位簽章來識別封裝的來源](security/identify-the-source-of-packages-with-digital-signatures.md)。  
  
 **如果封裝沒有簽章則顯示警告**  
 選取此選項即可在載入未簽署的封裝時顯示警告。  
  
 **顯示優先順序約束條件標籤**  
 選取在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中檢視封裝時，要在優先順序條件約束上顯示哪一個標籤 (成功、失敗或完成)。  
  
 **指令碼語言**  
 選取新指令碼工作和指令碼元件的預設指令碼語言。  
  
 **更新連接字串以使用新的提供者名稱**  
 在開啟或升級 [!INCLUDE[ssISversion2005](../includes/ssisversion2005-md.md)] 封裝時，請為目前版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]更新連接字串，以使用下列提供者的名稱：  
  
-   [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] OLE DB 提供者  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client  
  
 [ [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝升級精靈] 只會更新儲存在連線管理員中的連接字串。 此精靈不會更新使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 運算式語言或使用指令碼工作中之程式碼以動態方式建構的連接字串。  
  
 **建立新的封裝識別碼**  
 在升級 [!INCLUDE[ssISversion2005](../includes/ssisversion2005-md.md)] 封裝時，針對升級版本的封裝建立新的封裝識別碼。  
  
## <a name="see-also"></a>另請參閱  
 [安全性概觀&#40;Integration Services&#41;](security/security-overview-integration-services.md)   
 [使用指令碼擴充套件](extending-packages-scripting/extending-packages-with-scripting.md)  
  
  
