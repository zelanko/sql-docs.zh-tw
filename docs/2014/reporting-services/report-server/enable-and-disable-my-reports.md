---
title: 啟用與停用我的報表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- deactivated My Reports folder
- folders [Reporting Services], My Reports
- activated My Reports folder
- My Reports folder [Reporting Services]
- disabling My Reports folder
ms.assetid: 16c76e82-9fd4-417c-9ed3-a7d5bcd1dba2
caps.latest.revision: 36
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 56a4d317debae238ffc65cfcc04c72b8787421d9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134092"
---
# <a name="enable-and-disable-my-reports"></a>啟用與停用我的報表
  [我的報表] 功能會配置報表伺服器資料庫中的個人儲存區，讓使用者能夠將自己的報表儲存在私人資料夾內。 身為報表伺服器管理員，您可以啟用或停用此功能，或修改安全性設定 (此設定會控制使用者可以在其工作空間執行哪些動作) 來變更此功能的運作方式。  
  
 根據預設值，[我的報表] 功能是停用的。 您可以針對所有使用者啟用或停用此功能，但無法針對部份使用者啟用此功能。 大多數的使用者和組織都認為此功能很有用；請詳閱此主題稍後所呈現的優點及缺點，以決定此功能是否適合您的組織。  
  
## <a name="how-to-enable-and-disable-my-reports"></a>如何啟用與停用我的報表  
 若要使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]啟用 [我的報表]，連接到報表伺服器執行個體，然後開啟 **[伺服器屬性]** 頁面。 接著在 **[一般]** 索引標籤上，選取 **[為每個使用者啟用 [我的報表] 資料夾]** 選項。  
  
 [我的報表] 所使用的角色定義會決定 [我的報表] 工作空間所支援的動作。 例如，如果「我的報表」角色排除「建立連結報表」，則使用者無法在 [我的報表] 資料夾中建立連結報表。 如需詳細資訊，請參閱 [保護我的報表](../security/secure-my-reports.md)。  
  
 若要停用 [我的報表]，清除 **[為每個使用者啟用 [我的報表] 資料夾]**。 停用「我的報表」之後，將會移除所有與 [我的報表] 資料夾相關的可見項目。 停用此功能之後，必須手動移除實際用於儲存的資料夾 (亦即 [使用者資料夾] 中的子資料夾)。  
  
### <a name="when-my-reports-is-activated"></a>當啟動 [我的報表] 時  
 當此功能啟動時，使用者可以在根資料夾 (主資料夾) 中看到 [我的報表] 資料夾。 除了 [我的報表] 資料夾以外，報表伺服器管理員也可以看到包含每位使用者子資料夾的 [使用者資料夾] 資料夾。  
  
 此功能啟動期間，將無法刪除 [使用者資料夾] 及其子資料夾。 此外，[我的報表] 名稱將成為根節點 (主資料夾) 之下的資料夾保留名稱。  
  
 若您在停用 [我的報表] 之後重新啟動該功能，如果 [使用者資料夾] 資料夾不存在，報表伺服器就會建立一個新的 [使用者資料夾] 資料夾。 如果 [使用者資料夾] 已經存在，報表伺服器會在使用者登入其 [我的報表] 資料夾時建立新的子資料夾。  
  
### <a name="when-my-reports-is-deactivated"></a>當停用 [我的報表] 時  
 當此功能停用時，[我的報表] 名稱將不再保留；使用者可以在 [主資料夾] 資料夾之下建立名為 [我的報表] 的個人資料夾。 此外，將無法再重新導向我的報表至使用者特定之 [我的報表] 子資料夾。 最後，任何包含使用者特定之 [我的報表] 子資料夾的報表連結 URL 位址，將無法正常運作。  
  
## <a name="choosing-to-use-my-reports"></a>選擇使用 [我的報表]  
 是否使用 [我的報表]，取決於您是否想要有專屬的伺服器資源，來支援使用者工作空間。 [我的報表] 具有強大的功能，可以讓使用者掌控資訊資源，以協助他們完成工作。 它也提供使用者特殊的報表使用方式。 使用 [我的報表] 的重要原因之一，是它可以提供安全、易於管理的支援，給需要撰寫及檢視報表的使用者群組。 若無此功能，您可能會需要經常為不同的使用者，建立特定的資料夾和安全性原則。 隨著使用者及使用者需求的變更，此方式會使資料夾和原則數量隨著時間而增加，因而難以維護。  
  
 請注意，若您啟用「我的報表」，當網域帳戶的使用者按下 [我的報表] 連結時，報表伺服器就會為每一位使用者建立 [我的報表] 資料夾，即使使用者不想要或不需要 [我的報表] 資料夾。 目前沒有可判斷哪些資料夾正在使用的有效方法。 您必須手動檢視資料夾，以查看其中是否包含任何資料。  
  
## <a name="see-also"></a>另請參閱  
 [保護我的報表](../security/secure-my-reports.md)   
 [報表伺服器內容管理 &#40;SSRS 原生模式&#41;](report-server-content-management-ssrs-native-mode.md)  
  
  