---
title: 輸入密碼頁面 (新增複本精靈) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: availability-groups
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.addreplicawizard.enterpasswords.f1
ms.assetid: e69207a0-c5c4-44e4-ae9a-4afbb67251d1
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9222f0b5d941cbdac38dc04afc3f770c9d487029
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="enter-passwords-page-add-replica-wizard"></a>輸入密碼頁面 (加入複本精靈)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本說明主題描述 [輸入密碼] 頁面的選項。 本主題適用於 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 的 [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)]。  
  
 如果您在 [指定複本] 頁面上選取的複本包含具有資料庫主要金鑰的資料庫，則會顯示 [輸入密碼] 頁面。  
  
## <a name="enter-passwords-options"></a>輸入密碼選項  
 **[這個 SQL Server 執行個體上的使用者資料庫]** 方格會列出每個本機使用者資料庫。 資料行如下：  
  
 **名稱**  
 顯示本機使用者資料庫的名稱。  
  
 **大小**  
 顯示資料庫大小 (如果精靈可使用大小)。  
  
 **狀態**  
 針對具有資料庫主要金鑰的資料庫指出 [需要密碼]。 在 [密碼] 資料行中輸入資料庫主要金鑰的密碼之後，按一下 [重新整理]。 如果您已正確地輸入密碼，[狀態] 資料行會指出 [已輸入密碼]。  
  
 如果資料庫沒有資料庫主要金鑰，[狀態] 資料行會指出 [不需要密碼]。  
  
 **密碼**  
 如果 [狀態] 資料行指出 [需要密碼]，請輸入資料庫主要金鑰的密碼。  
  
 **[重新整理]**  
 按一下以重新整理方格。 輸入必要的密碼之後，這非常有用。  
  
## <a name="related-tasks"></a>相關工作  
  
-   [使用 [將複本加入可用性群組中精靈] &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>另請參閱  
 [Always On 可用性群組的必要條件、限制和建議 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
