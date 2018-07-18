---
title: 保護共用資料集項目的安全 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: security
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 08e6d8b5-d88c-4ed2-9c05-55c757e00014
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: dff365e2bee4f15ef72892d2a80fa7759161644d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33029635"
---
# <a name="secure-shared-dataset-items"></a>保護共用資料集項目的安全
  在報表伺服器上，共用資料集項目可由多個報表使用。 您可以保護共用資料集來控制使用者能夠存取的程度。 依預設，只有屬於 **管理員** 內建群組成員的使用者才可以檢視共用資料集、修改屬性、啟用快取、建立快取重新整理計劃，以及刪除項目。 其他所有使用者都必須具有針對他們所建立的角色指派，才能存取共用資料集。  
  
 若要設定安全性，請建立角色指派以指定能夠存取共用資料集的使用者或群組帳戶。  
  
## <a name="role-based-access-to-shared-datasets"></a>基於角色授與的共用資料集存取權  
 若要授與共用資料集的存取權，您可以讓使用者從父資料夾繼承現有的角色指派，或是在項目本身上建立新的角色指派。  
  
 可讓您加入、刪除、編輯項目屬性，並檢視資料集相關報表和共用資料來源的預設角色指派有：[內容管理員]、[我的報表] 和 [發行者]。 若要編輯共用資料集定義，請使用預設角色指派報表產生器或內容管理員。  
  
 由於角色指派通常是繼承自父節點，已啟用 [檢視報表]  工作的資料夾會傳承資料夾中之共用資料集和報表的權限。  
  
 若要就共用資料集及其查詢結果提供更強的控制，請在共用資料集項目上設定項目層級安全性，或將共用資料集儲存到資料夾，並在資料夾上設定項目層級安全性。  
  
## <a name="shared-dataset-parameters"></a>共用資料集參數  
 共用資料集參數無法用來為特定的使用者限制資料。 共用資料集參數之目的在於提供方法來指定處理共用資料集時要包含的資料。 在報表伺服器上，您不能保護共用資料集參數的值。  
  
 在共用資料集定義中，您可以將參數標示為唯讀，並指定預設值。 標示為唯讀的參數無法在伺服器上覆寫。 例如，在共用資料集的快取重新整理規劃中，您無法指定唯讀參數的值。 如果共用資料集參數包含參考使用者全域集合的運算式，或是與任何其他使用者有相依性，您就無法為共用資料集建立快取重新整理計劃。  
  
## <a name="tasks-access-to-items-and-default-roles"></a>工作、項目存取權與預設角色  
 共用資料集遵循與報表相同的安全性模型。 若要提供使用者特定動作的權限，請選擇包含該權限之對應工作的角色。 下表列出其中所包含工作和動作。  
  
|選取的工作|授與的權限|包含工作的預設角色|  
|----------------------|---------------------------------|-----------------------------------------|  
|檢視報表|檢視資料夾階層中的共用資料集項目。 如果沒有此工作，使用者就看不到項目，也可能不知道有資料集可以使用。|瀏覽器<br /><br /> 內容管理員<br /><br /> 報表產生器<br /><br /> 我的報表|  
|管理報表|檢視指定名稱、描述和連接資訊的屬性。 此工作也用來顯示資料夾階層中的共用資料集項目。 如果選擇此工作，可以省略「檢視報表」工作。|內容管理員<br /><br /> 發行者<br /><br /> 我的報表|  
|取用報表|檢視共用資料集定義。|內容管理員<br /><br /> 報表產生器|  
|設定項目安全性|建立及修改控制共用資料集存取權的角色指派。 此工作必須配合「檢視報表」或「管理報表」工作使用。 如果不是，則因為使用者無法選取項目，而沒有作用。|內容管理員|  
  
 如需詳細資訊，請參閱 [項目層級工作](../../reporting-services/security/tasks-and-permissions-item-level-tasks.md) 和 [預先定義的角色](../../reporting-services/security/role-definitions-predefined-roles.md)。  
  
## <a name="see-also"></a>另請參閱  
 [管理共用資料集](../../reporting-services/report-data/manage-shared-datasets.md)   
 [保護資料夾的安全](../../reporting-services/security/secure-folders.md)   
 [保護報表和資源的安全](../../reporting-services/security/secure-reports-and-resources.md)   
 [在原生模式報表伺服器上授與權限](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [在原生模式報表伺服器上授與權限](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
