---
title: 工作與權限 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], tasks
- role-based security [Reporting Services], permissions
- security [Reporting Services], tasks
- security [Reporting Services], permissions
- role-based security [Reporting Services], tasks
- predefined tasks [Reporting Services]
- tasks [Reporting Services]
ms.assetid: d7ff90b5-b976-4270-b9ad-9d7b801d8263
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5ec2030e94abbc568e2ea030c781e904a4ce459d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63306166"
---
# <a name="tasks-and-permissions"></a>工作和權限
  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中，「工作」(Task) 是使用者或管理員可以執行的動作。 工作是預先定義的。 您無法建立自訂工作或修改以程式設計的方式或透過工具而提供的工作。 總共有 25 種工作。 這些工作構成以角色為基礎之安全性中，可以使用的整個作業集。 工作的範例包括「檢視報表」、「管理報表」以及「管理報表伺服器屬性」。  
  
 每一個工作包含一組也是預先定義的權限。 例如，「管理資料夾」工作包含建立和刪除資料夾，以及檢視和更新資料夾屬性的權限。 每一種工作的權限都有文件說明，以提供每一種工作的更精確描述。 無法直接與權限互動，或在角色指派中指定權限。 使用者是透過包括在角色定義中的工作，間接被授與權限。  
  
 唯有工作屬於角色的一部份，而該角色包含在角色指派中時，才能執行工作。 因此，角色中若未包含檢視模型工作，或該角色未包含在角色指派中，使用者就無法檢視報表模型。 下列圖表顯示如何將權限結合到工作中，以及如何將工作結合到可用於特定角色指派的角色中。  
  
 ![權限和工作圖表](../media/report-securityobjects.gif "權限和工作圖表")  
權限和工作圖表  
  
## <a name="system-and-item-level-tasks"></a>系統和項目層級工作  
 工作分成兩個類別目錄：系統層級和項目層級。 角色可以包括僅來自單一類別目錄的工作。 下表描述每一種類別目錄的工作。  
  
|Category|描述|  
|--------------|-----------------|  
|[項目層級工作](tasks-and-permissions-item-level-tasks.md)|在資料夾、報表、報表模型和資源等受到報表伺服器管理之項目上執行的動作。<br /><br /> 項目層級工作的範圍為報表伺服器資料夾命名空間。 您透過報表伺服器上的資料夾，或者透過 URL 存取的所有項目，都受到包含項目層級工作之角色指派的保護。|  
|[系統層級工作](tasks-and-permissions-system-level-tasks.md)|在系統層級執行的動作，例如管理作業或可以用於許多項目的共用排程。 系統層級工作的範圍是在報表伺服器資料夾命名空間以外。|  
  
## <a name="see-also"></a>另請參閱  
 [角色定義](role-definitions.md)   
 [Predefined Roles](role-definitions-predefined-roles.md)   
 [在原生模式報表伺服器上授與權限](granting-permissions-on-a-native-mode-report-server.md)  
  
  
