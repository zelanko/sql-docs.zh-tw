---
title: "為 CDC 準備 SQL Server |Microsoft 文件"
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
- prepSqlSrv
ms.assetid: 20b51dbf-a545-4234-87ae-4228268a0fb2
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 29eee5c85a323e70dab3ac9bdb25bd72820b0489
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="prepare-sql-server-for-cdc"></a>為 CDC 準備 SQL Server
  Oracle CDC 服務要求所有目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體都必須包含 MSXDBCDC 資料庫。 您可在 CDC 服務組態主控台中使用「準備 SQL Server」動作來建立這個資料庫。 這樣會建立特殊指令碼，可執行該指令碼來針對這個資料庫建立必要資料表、預存程序和其他必要成品。 這個工作只會針對每個目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體執行一次。  
  
 如需有關 MSXDBCDC 資料庫的詳細資訊，請參閱＜MSXDBCDC 資料庫＞。  
  
 在 CDC 服務組態主控台中，按一下 [Prepare SQL Server (準備 SQL Server)]。 如果無法使用這個選項，請確定已在主控台的左窗格選取 [Local CDC Services (本機 CDC 服務)]。  
  
## <a name="options"></a>選項。  
  
### <a name="server-name"></a>伺服器名稱  
 輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所在的伺服器名稱。  
  
### <a name="authentication"></a>驗證  
 選取下列其中一項：  
  
-   **Windows 驗證**  
  
-   **SQL Server 驗證**：如果您選取這個選項，您必須針對您所連接之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的使用者輸入 [使用者名稱] 和 [密碼]。  
  
 若要針對 Oracle CDC 準備 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，登入必須擁有 MSXDBCDC 資料庫的寫入權限。 請輸入擁有 MSXDBCDC 資料庫寫入權限之登入的認證，例如 `sysasmin` 角色的成員。  
  
### <a name="options"></a>選項。  
 按一下箭頭即可檢視要設定的可用選項。 您可以選擇保留這些選項的預設值。 可用的選項如下：  
  
-   **連接逾時**：輸入 Oracle CDC 服務在逾時之前，等候連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的時間 (以秒數為單位)。 預設值為 **15**。  
  
-   **執行逾時**：輸入 Oracle CDC Windows 服務在逾時之前，等候執行命令的時間 (以秒數為單位)。 預設值是 **30**。  
  
-   **加密連接**：針對 Oracle CDC 服務與使用加密連接之目標 **執行個體之間的通訊選取** [加密連接] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   **進階**：必要時輸入其他任何連接屬性。  
  
### <a name="view-script"></a>檢視指令碼  
 按一下 [檢視指令碼]，檢視安裝指令碼的唯讀版本。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員可以將此指令碼複製到 SQL Server 管理主控台來進行編輯 (必要的話)。 如需準備 SQL Server 指令碼的詳細資訊，請參閱 [為 Oracle CDC 檢視指令碼準備 SQL Server](../../integration-services/change-data-capture/prepare-sql-server-for-oracle-cdc-view-script.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [如何使用 CDC 服務](../../integration-services/change-data-capture/how-to-work-with-cdc-services.md)   
 [如何為 CDC 準備 SQL Server](../../integration-services/change-data-capture/how-to-prepare-sql-server-for-cdc.md)  
  
  
