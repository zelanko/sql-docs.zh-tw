---
title: 傳送登入工作編輯器（登入頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferloginstask.logins.f1
helpviewer_keywords:
- Transfer Logins Task Editor
ms.assetid: bf244c24-bd45-4ece-b66b-78b488f35c5b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ae8ebf56e4ae7c4fce3566cb7688d203b8ceb318
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66054930"
---
# <a name="transfer-logins-task-editor-logins-page"></a>傳送登入工作編輯器 (登入頁面)
  使用 [傳送登入工作編輯器]**** 對話方塊的 [登入]**** 頁面，即可指定屬性將一個或多個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 登入，從 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的一個執行個體複製到另一個執行個體。 如需這項工作的詳細資訊，請參閱 [傳送登入工作](control-flow/transfer-logins-task.md)。  
  
> [!IMPORTANT]  
>  執行傳送登入工作時，目的地伺服器上會建立具隨機密碼的登入，且會停用這些密碼。 若要使用這些登入， **系統管理員** 固定伺服器角色的成員就必須變更密碼，然後啟用密碼。 無法傳送**sa**登入。  
  
## <a name="options"></a>選項。  
 **SourceConnection**  
 在清單中選取 SMO 連線管理員，或按一下** \<[新增連接 ...] >** ，建立與來源伺服器的新連接。  
  
 **[Destinationconnection**  
 在清單中選取 SMO 連線管理員，或按一下** \<[新增連接 ...] >** ，以建立目的地伺服器的新連接。  
  
 **LoginsToTransfer**  
 選取要從來源複製到目的地伺服器的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 登入。 此屬性具有下表所列的選項：  
  
|值|描述|  
|-----------|-----------------|  
|**AllLogins**|來源伺服器上的所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 登入，都會複製到目的地伺服器。|  
|**SelectedLogins**|只有使用 **LoginsList** 指定的登入，才會複製到目的地伺服器。|  
|**AllLoginsFromSelectedDatabases**|使用 **DatabasesList** 指定之資料庫中的所有登入，都會複製到目的地伺服器。|  
  
 **Loginslist 才**  
 選取來源伺服器上要複製到目的地伺服器的登入。 唯有針對 [LoginsToTransfer]**** 選取了 [SelectedLogins]**** 時，才能使用此選項。  
  
 **DatabasesList**  
 選取來源伺服器上的資料庫，其中包含要複製到目的地伺服器的登入。 唯有針對 [LoginsToTransfer]**** 選取了 [AllLoginsFromSelectedDatabases]**** 時，才能使用此選項。  
  
 **IfObjectExists**  
 選取工作應如何處理已經存在於目的地伺服器上，且具有相同名稱的登入。  
  
 此屬性具有下表所列的選項：  
  
|值|描述|  
|-----------|-----------------|  
|**FailTask**|如果具有相同名稱的登入已經存在於目的地伺服器上，工作就會失敗。|  
|**Overwrite**|工作會覆寫目的地伺服器上具有相同名稱的登入。|  
|**Skip**|工作會略過目的地伺服器上具有相同名稱的登入。|  
  
 **Copysids 就**  
 選取與登入相關聯的安全性識別碼，是否應複製到目的地伺服器。 如果「傳送登入」工作與「傳送資料庫」工作一起使用，則**copysids 就**必須設定為**True** 。 否則，已傳送的資料庫就無法辨識被複製的登入。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 工作](control-flow/integration-services-tasks.md)   
 [[傳送登入工作編輯器] &#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [運算式頁面](expressions/expressions-page.md)   
 [SMO 連線管理員](connection-manager/smo-connection-manager.md)   
 [增強式密碼](../relational-databases/security/strong-passwords.md)   
 [SQL Server 安裝的安全性考量](../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
