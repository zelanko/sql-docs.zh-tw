---
title: 建立及編輯 Oracle CDC 服務 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- createSrv
ms.assetid: 10cd612e-d8f1-4af2-97d3-a0c22e1e2326
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e362438b12c103dd6210766da888086da79df126
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52785460"
---
# <a name="create-and-edit-an-oracle-cdc-service"></a>建立及編輯 Oracle CDC 服務
  您會從 CDC 服務組態主控台來建立和編輯新的 Oracle CDC Windows 服務。  
  
 若要建立新的 Oracle CDC Windows 服務，請從左窗格選取 **[本機 CDC 服務]** ，然後按一下 **[動作]** 窗格中的 **[新增服務]** 。 您也可以用滑鼠右鍵按一下 [本機 CDC 服務]，並選取 [新增服務]。 隨即開啟 [新增 Oracle CDC Windows 服務] 對話方塊。  
  
 **OR**  
  
 若要編輯 CDC 服務屬性，請選取您要編輯屬性的服務，然後按一下 **[動作]** 窗格中的 **[屬性]** 。 您也可以用滑鼠右鍵按一下您要使用的服務，然後選取 [屬性]。 [CDC 服務屬性] 對話方塊隨即開啟。  
  
 在 [新增 Oracle CDC Windows 服務] 對話方塊或 [CDC 服務屬性] 對話方塊中輸入以下資訊。  
  
 服務名稱  
 輸入新的 Oracle CDC Windows 服務名稱。 盡可能不要使用完整名稱。 不能在服務名稱中使用 / 和 \ 字元。  
  
> [!NOTE]  
> 當您編輯此服務時，不可使用這個選項。 您不能變更已經存在的 Windows 服務名稱。  
  
 **說明**  
 請輸入此服務的描述來加以識別。  
  
 **服務帳戶**  
 選取下列其中一項，以判斷執行此服務所要使用的帳戶：  
  
-   **本機系統帳戶**  
  
     不建議使用這項，因為它提供此服務的權限太多。  
  
-   **這個帳戶**  
  
     在 Windows Vista 或 Windows Server 2008 上，預設服務帳戶為 NETWORK SERVICE 帳戶。  
  
     在 Windows 7、Windows Server 2008 R2 及更新版本上，預設服務帳戶為 NT Service\\<服務名稱>。  
  
     使用這些帳戶讓您不需使用密碼即可工作，因為這些帳戶不需要密碼。 此外，這些帳戶只會提供 Oracle CDC 服務執行所需的必要權限。  
  
     您可以針對此服務帳戶使用本機或網域 Windows 帳戶。 在此情況下，您必須針對該帳戶輸入 **[密碼]** 。 此帳戶可適用於本機主機或網域帳戶。 在 Windows [控制台] 中使用本機服務變更密碼時，請務必更新密碼。  
  
 **伺服器名稱**:選取目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連接到的執行個體 (例如 **\\ \\< 電腦名稱 >\\< instance_name >**)。 預設會顯示上次連接的伺服器執行個體。  
  
 **驗證**  
 選取下列其中一項：  
  
-   **Windows 驗證**:如果您選取此選項時，Oracle CDC 服務會連接到目標[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體使用的服務帳戶身分識別。 如果正在另一部電腦上執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，必須搭配網域帳戶使用 Windows 驗證。  
  
-   **SQL Server 驗證**:如果您選取此選項時，您必須輸入**使用者名**並**密碼**如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您想要使用的登入。 Oracle CDC 服務會在連接到目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時使用這些認證。  
  
 Oracle CDC 服務所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入只要求它必須是公用固定伺服器角色的成員，不需要其他權限。 一旦加入新的 Oracle CDC 執行個體之後，該登入會取得關聯 **CDC 資料庫的** db_owner [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存取權。  
  
 若要建立 Oracle CDC Windows 服務定義，此程式需要關聯 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中 MSXDBCDC 資料庫的更新存取權。 當您按一下 **[確定]** 時，隨即出現一個對話方塊，提示使用者輸入具有 MSXDBCDC 資料庫之更新存取權的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
 如需有關您必須在 [連接到 SQL Server] 對話方塊中輸入之資料的詳細資訊，請參閱＜ [Connection to SQL Server](connection-to-sql-server.md)＞。  
  
 **選項。**  
 按一下箭頭即可檢視要設定的可用選項。 您可以選擇保留這些選項的預設值。 可用的選項如下：  
  
-   **連接逾時**:輸入 Oracle CDC 服務在逾時之前等候連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的時間 (以秒數為單位)。預設值為 **15**。  
  
-   **執行逾時**:輸入 Oracle CDC Windows 服務在逾時之前，等候執行命令的時間 (以秒數為單位)。預設值是 **30**。  
  
-   **加密連接**:選取 **加密連接**Oracle CDC 服務與目標之間的通訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體使用加密的連線。  
  
-   **進階**：如有必要，請輸入任何其他連接屬性。  
  
 **主要密碼**  
 輸入 Oracle CDC Windows 服務為了保護 Oracle 記錄採礦認證所使用的密碼。  
  
 在高可用性組態叢集的其他節點上設定相同服務的其他執行個體時，也必須使用相同的主要密碼。 如果您遺失或修改主要密碼，則儲存在 Oracle CDC 執行個體資料庫中的所有記錄採礦密碼都必須使用 CDC 設計工具主控台重新輸入。  
  
## <a name="see-also"></a>另請參閱  
 [如何建立及編輯 CDC 服務](how-to-create-and-edit-a-cdc-service.md)  
  
  
