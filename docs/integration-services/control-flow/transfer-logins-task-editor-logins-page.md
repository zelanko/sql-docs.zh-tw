---
title: "傳送登入工作編輯器 （登入頁面） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.transferloginstask.logins.f1
helpviewer_keywords:
- Transfer Logins Task Editor
ms.assetid: bf244c24-bd45-4ece-b66b-78b488f35c5b
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cdae4242ff131376f8aba2bd4a1ec4fc08170ecd
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="transfer-logins-task-editor-logins-page"></a>傳送登入工作編輯器 (登入頁面)
  使用 [傳送登入工作編輯器] 對話方塊的 [登入] 頁面，即可指定屬性將一個或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的一個執行個體複製到另一個執行個體。 如需這項工作的詳細資訊，請參閱[傳送登入工作](../../integration-services/control-flow/transfer-logins-task.md)。  
  
> [!IMPORTANT]  
>  執行傳送登入工作時，目的地伺服器上會建立具隨機密碼的登入，且會停用這些密碼。 若要使用這些登入， **系統管理員** 固定伺服器角色的成員就必須變更密碼，然後啟用密碼。 無法傳送 **sa** 登入。  
  
## <a name="options"></a>選項。  
 **SourceConnection**  
 在清單中，選取一個 SMO 連接管理員，或按一下**\<新增連接 … >**來建立新的連接到來源伺服器。  
  
 **DestinationConnection**  
 在清單中，選取一個 SMO 連接管理員，或按一下**\<新增連接 … >**來建立新的連接到目的地伺服器。  
  
 **LoginsToTransfer**  
 選取要從來源複製到目的地伺服器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 此屬性具有下表所列的選項：  
  
|Value|說明|  
|-----------|-----------------|  
|**AllLogins**|來源伺服器上的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，都會複製到目的地伺服器。|  
|**SelectedLogins**|只有使用 **LoginsList** 指定的登入，才會複製到目的地伺服器。|  
|**AllLoginsFromSelectedDatabases**|使用 **DatabasesList** 指定之資料庫中的所有登入，都會複製到目的地伺服器。|  
  
 **LoginsList**  
 選取來源伺服器上要複製到目的地伺服器的登入。 唯有針對 [LoginsToTransfer] 選取了 [SelectedLogins] 時，才能使用此選項。  
  
 **DatabasesList**  
 選取來源伺服器上的資料庫，其中包含要複製到目的地伺服器的登入。 唯有針對 [LoginsToTransfer] 選取了 [AllLoginsFromSelectedDatabases] 時，才能使用此選項。  
  
 **IfObjectExists**  
 選取工作應如何處理已經存在於目的地伺服器上，且具有相同名稱的登入。  
  
 此屬性具有下表所列的選項：  
  
|Value|說明|  
|-----------|-----------------|  
|**FailTask**|如果具有相同名稱的登入已經存在於目的地伺服器上，工作就會失敗。|  
|**Overwrite**|工作會覆寫目的地伺服器上具有相同名稱的登入。|  
|**Skip**|工作會略過目的地伺服器上具有相同名稱的登入。|  
  
 **CopySids**  
 選取與登入相關聯的安全性識別碼，是否應複製到目的地伺服器。 如果「傳送登入」工作是與「傳送資料庫」工作一併使用，[CopySids] 就必須設定為 [True]。 否則，已傳送的資料庫就無法辨識被複製的登入。  
  
## <a name="see-also"></a>請參閱＜  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)   
 [傳送登入工作編輯器 &#40;一般頁面 &#41;](../../integration-services/control-flow/transfer-logins-task-editor-general-page.md)   
 [運算式頁面](../../integration-services/expressions/expressions-page.md)   
 [SMO 連接管理員](../../integration-services/connection-manager/smo-connection-manager.md)   
 [增強式密碼](../../relational-databases/security/strong-passwords.md)   
 [SQL Server 安裝的安全性考量](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
