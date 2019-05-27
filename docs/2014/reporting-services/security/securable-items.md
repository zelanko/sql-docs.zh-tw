---
title: 安全性實體項目 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- securable items [Reporting Services]
- roles [Reporting Services], securable items
- security [Reporting Services], securable items listed
- role-based security [Reporting Services], securable items
ms.assetid: 27f58d4c-5c7b-4947-af5b-0f1fa60faf5f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4c5c4d515ebe6aa9b4b8120ae909f07dccc74de0
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66101703"
---
# <a name="securable-items"></a>安全性實體項目
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會使用以角色為基礎的安全性，控制儲存在報表伺服器上之項目的存取權。 當您授與使用者對報表伺服器的存取權時，您通常會建立一對角色指派來進行此動作：  
  
-   在網站層級上。  
  
-   在主資料夾上，這是報表伺服器資料夾階層的根節點。  
  
 安全性會在報表伺服器資料夾階層中繼承。 在網站層級和主資料夾上建立角色指派，會設定可擴充至所有項目的權限繼承及報表伺服器上的作業。  
  
 您可以為個別項目定義安全性，以覆寫權限繼承。 您可以個別維護安全的項目包括：  
  
-   資料夾  
  
-   報表  
  
-   報表模型  
  
-   資源  
  
-   共用資料來源  
  
-   共用資料集  
  
 其他建構 (例如排程與訂閱) 並未明確保護。 排程與訂閱是在報表的安全性內作業。  
  
## <a name="item-descriptions"></a>項目描述  
 下表列出安全性實體項目並敘述它們的特性。  
  
|項目|特性|  
|----------|---------------------|  
|資料夾|資料夾安全性會套用至資料夾本身以及它包含的項目。 [主資料夾] 資料夾是資料夾階層的根節點。 此資料夾所設定的安全性，會為資料夾階層中所有從屬的資料夾、報表、資源和共用資料來源，建立初始安全性設定。 如需詳細資訊，請參閱 [保護資料夾的安全](secure-folders.md)。<br /><br /> [我的報表] 是特殊用途資料夾，可以透過以專用角色為基礎的隱含角色指派來保護。 如需詳細資訊，請參閱 [保護我的報表](secure-my-reports.md)。|  
|報表|可以保護報表與連結報表，以控制使用者可以執行之動作的範圍，例如變更給定報表的屬性。<br /><br /> 報表記錄是透過包含記錄的報表來保護。 您無法保護報表記錄內的個別快照集。<br /><br /> 如需保護報表的詳細資訊，請參閱 [保護報表和資源的安全](secure-reports-and-resources.md)。|  
|報表模型|您可以在全部或部分的報表模型上，指定角色指派。 因為報表模型可能很龐大，所以您可能要保護對應至機密資料的模型項目。|  
|資源|可以保護資源，來控制資源本身與其屬性的存取。<br /><br /> 只有獨立的資源可以當成個別項目來保護。 內嵌在報表中的資源，無法與報表分開保護。<br /><br /> 如需資源安全性的詳細資訊，請參閱 [保護報表和資源的安全](secure-reports-and-resources.md)。|  
|共用資料來源|共用資料來源可以進行保護，以限制對項目及其屬性頁面的存取。 如需詳細資訊，請參閱 [保護共用資料來源項目的安全](secure-shared-data-source-items.md)。|  
|共用資料集|共用資料集可以進行保護，以控制使用者能夠執行的動作範圍，例如，檢視或變更定義，或變更指定共用資料集的屬性。<br /><br /> 如需詳細資訊，請參閱 [保護共用資料集項目的安全](secure-shared-dataset-items.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [在原生模式報表伺服器上授與權限](granting-permissions-on-a-native-mode-report-server.md)   
 [建立、刪除或修改角色 &#40;Management Studio&#41;](role-definitions-create-delete-or-modify.md)   
 [將報表伺服器的存取權授與使用者 &#40;報表管理員&#41;](grant-user-access-to-a-report-server.md)   
 [修改或刪除角色指派 &#40;報表管理員&#41;](role-assignments-modify-or-delete.md)  
  
  
