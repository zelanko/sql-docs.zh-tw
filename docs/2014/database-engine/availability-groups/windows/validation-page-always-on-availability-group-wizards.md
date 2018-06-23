---
title: 驗證頁面 （AlwaysOn 可用性群組精靈） |Microsoft 文件
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.newagwizard.validation.f1
- sql12.swb.addreplicawizard.validation.f1
- sql12.swb.adddatabasewizard.validation.f1
helpviewer_keywords:
- ', listeners'
ms.assetid: c8971556-240c-491a-bc86-9cc72f71a3dd
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: 6a786543983739efe940631ab05be4d41ab5798e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136067"
---
# <a name="validation-page-alwayson-availability-group-wizards"></a>驗證頁面 (AlwaysOn 可用性群組精靈)
  本說明主題描述 [驗證] 頁面的選項。 本主題適用於 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] 的[!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)]、[!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)]和[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。 使用此頁面可以驗證環境是否支援您在精靈之先前頁面上所做的所有組態選擇。  
  
##  <a name="PageOptions"></a> 驗證頁面選項  
 **可用性群組驗證的結果。**  
 此方格會顯示每個已完成驗證步驟的結果。 方格資料行如下所示：  
  
 **名稱**  
 顯示描述特定步驟的片語。  
  
 **結果**  
 顯示下列其中一個超連結文字。 如需有關給定驗證步驟之結果的詳細資訊，請按一下超連結。  
  
|結果|描述|  
|------------|-----------------|  
|**錯誤**|表示驗證步驟失敗。 按一下連結可檢視錯誤訊息。|  
|**已略過**|表示已略過驗證步驟，因為您的選項不需要驗證。 按一下連結可檢視略過步驟的原因。|  
|**成功**|表示驗證步驟已順利完成。|  
|**警告**|表示可用性群組組態可能有問題。  按一下連結可檢視警告訊息。|  
  
 **重新執行驗證**  
 如果您在精靈外部進行變更以回應驗證錯誤，按一下可重複驗證步驟。  
  

  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [使用新增可用性群組對話方塊 &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [使用 [將複本加入可用性群組中精靈] &#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [使用將資料庫加入至可用性群組精靈 &#40;SQL Server Management Studio&#41;](availability-group-add-database-to-group-wizard.md)  
  
 
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  