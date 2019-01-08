---
title: 保護我的報表 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- denying My Reports folder access
- private folders [Reporting Services]
- user workspace [Reporting Services]
- security [Reporting Services], My Reports folder
- My Reports folder [Reporting Services]
ms.assetid: 3b23a382-13b8-4196-9a93-7fe62d03a63c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7d80ec6d5087735602b05326e874263c083657a6
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53211467"
---
# <a name="secure-my-reports"></a>保護我的報表
  [我的報表] 功能會提供用於報表之使用者管理的工作空間。 為達成其目的，[我的報表] 資料夾的權限，應較一般用途的其他資料夾為寬鬆。 使用者如果只有檢視及執行其他資料夾中之報表的權限，則需要一組擴充的權限來管理其 [我的報表] 資料夾和擁有的內容。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供此用途的特殊角色指派及角色定義。  
  
> [!NOTE]
>  只有在報表管理員中，才能使用 [我的報表]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中無法使用它。  
  
## <a name="role-assignment-for-my-reports"></a>[我的報表] 的角色指派  
 [我的報表] 的角色指派有預先設定的元素，而且是為啟用 [我的報表] 資料夾的每一個使用者自動建立的。 讓報表伺服器自動指派安全性，對於廣泛使用 [我的報表] 的組織特別有用，因為管理員不必啟用每個 [我的報表] 使用者的存取權。  
  
 **我的報表** 角色指派是由下列元素組成：  
  
-   使用者的 [我的報表] 資料夾，位於 Users Folders\\\<使用者名稱>\My Reports 資料夾內。  
  
-   使用者帳戶，會判斷何時啟用 [我的報表] 資料夾。 資料夾是當使用者按一下報表管理員的 [我的報表] 資料夾，或者從報表設計師發行報表至 [我的報表] 資料夾時啟用。 此資料夾也會在使用者要求 [我的報表] 連結的屬性時啟用。  
  
-   [我的報表] 之預先定義的角色定義。  
  
## <a name="role-definition-for-my-reports"></a>[我的報表] 的角色定義  
 **我的報表** 角色定義包含支援 [我的報表] 資料夾之內容管理的工作。 **我的報表** 角色旨在作為單一用途角色。 雖然您在任何項目層級的安全性原則中都能選擇此角色，不過應該避免此動作，盡量不要為了配合其他資料夾需求而修改。 保留 [我的報表] 功能的 **我的報表** 角色，能夠協助您維護使用者經驗的一致性。  
  
 依預設，只有報表伺服器管理員能夠修改 **我的報表** 角色。 您可以變更 **我的報表** 角色所包含的工作，以此來自訂角色。 您也可以替代其他角色。  
  
## <a name="denying-access-to-my-reports"></a>拒絕存取 [我的報表]  
 您可以禁止使用者存取 [我的報表]，方法是：  
  
-   在 [站台設定] 頁面上停用 [我的報表]。 如需詳細資訊，請參閱 [啟用與停用我的報表](../../reporting-services/report-server/enable-and-disable-my-reports.md)。  
  
-   移除 **我的報表** 角色中的所有工作。  
  
 當您停用 [我的報表] 時，會從報表管理員移除 [我的報表] 資料夾的連結。 支援 [我的報表] 的基礎資料夾結構 (亦即，[使用者資料夾] 資料夾和子資料夾) 仍然可以使用，而且若使用者知道資料夾路徑，也可以存取。 從 **我的報表** 角色移除工作，可確保禁止存取。  
  
## <a name="see-also"></a>另請參閱  
 [保護報表和資源的安全](../../reporting-services/security/secure-reports-and-resources.md)   
 [保護資料夾的安全](../../reporting-services/security/secure-folders.md)   
 [在原生模式報表伺服器上授與權限](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
