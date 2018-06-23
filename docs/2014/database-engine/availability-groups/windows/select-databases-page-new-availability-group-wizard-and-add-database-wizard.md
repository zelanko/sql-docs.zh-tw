---
title: 選取資料庫頁面 （新增可用性群組精靈加入資料庫精靈） |Microsoft 文件
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
- sql12.swb.adddatabasewizard.selectdatabases.f1
- sql12.swb.newagwizard.selectdatabases.f1
ms.assetid: 929c5e15-d087-438d-b1f2-aa97c5f8bff8
caps.latest.revision: 12
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 304ce826a45debaf4d18a63e9d68061ef393705b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133312"
---
# <a name="select-databases-page-new-availability-group-wizard-add-database-wizard"></a>選取資料庫頁面 （新增可用性群組精靈加入資料庫精靈）
  本說明主題描述 **[指定資料庫]** 頁面的選項。 此主題適用於 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] 的 [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] 和 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。  
  
##  <a name="PageOptions"></a> 選取資料庫選項  
 **[這個 SQL Server 執行個體上的使用者資料庫]** 方格會列出每個本機使用者資料庫。 資料行如下：  
  
 **名稱**  
 顯示本機使用者資料庫的名稱。  
  
 **大小**  
 顯示資料庫大小 (如果精靈可使用大小)。  
  
 **狀態**  
 顯示超連結，其文字指出給定的資料庫是否符合加入可用性群組的必要條件。 如果狀態為 **[符合必要條件]**，表示您可以將此資料庫加入至可用性群組。 如果資料庫不符合所有必要條件， **[狀態]** 超連結會提供為什麼資料庫不合格的簡短說明。 如需詳細資訊，請按一下此超連結。  
  
 對資料庫採取動作以符合必要條件時，您可以離開精靈的 **[選取資料庫]** 頁面。 當您返回 **[選取資料庫]** 頁面時，請按一下 **[重新整理]** 更新方格。  
  
 **[重新整理]**  
 按一下以重新整理方格。 對資料庫採取動作以符合必要條件之後，這非常有用。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [使用新增可用性群組對話方塊 &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [使用將資料庫加入至可用性群組精靈 &#40;SQL Server Management Studio&#41;](availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [必要條件、 限制和建議的 AlwaysOn 可用性群組&#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
  
  