---
title: "連接到 SQL Server 進行刪除 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 030b10c2-6b88-4c2c-bf67-22994be25a60
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9be0eb89c1d19068e8cb97e94654d5dc177c0a86
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="connection-to-sql-server-for-delete"></a>連接到 SQL Server 進行刪除
  如果登入沒有包含 MSXDBCDC 資料庫之寫入權限的資料庫角色 (例如 **db_owner** 角色)，則當此登入嘗試刪除 Oracle CDC 執行個體時，便會顯示 [連接到 SQL Server] 對話方塊。  
  
 在此對話方塊中，您必須輸入擁有 MSXDBCDC 資料庫寫入權限之登入的認證 (例如 **db_owner** 資料庫角色)，才能刪除 Oracle CDC 執行個體。  
  
 在 [連接到 SQL Server] 對話方塊中輸入以下資訊。  
  
 **伺服器名稱**  
 輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所在的伺服器名稱。  
  
 **驗證**  
 選取下列其中一項：  
  
-   **Windows 驗證**  
  
-   **SQL Server 驗證**：如果您選取這個選項，您必須針對您所連接之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的使用者輸入 [登入] 和 [密碼]。  
  
 **選項。**  
 按一下箭頭即可檢視要設定的可用選項。 您可以選擇保留這些選項的預設值。 可用的選項如下：  
  
-   **連接逾時**：輸入此程式在產生逾時錯誤之前，等候連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的時間 (以秒數為單位)。 預設值為 **15**。  
  
-   **執行逾時**：輸入此程式在產生逾時錯誤之前，等候執行 SQL 命令的時間 (以秒數為單位)。 預設值是 **30**。  
  
-   **加密連接**：選取 [加密連接]，以確保正在建立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接已加密來保障隱私權。  
  
-   **進階**：按一下 [進階]，並在必要時，於 [進階連接屬性] 對話方塊中輸入其他任何連接屬性。  
  
## <a name="see-also"></a>另請參閱  
 [CDC 服務 SQL Server 連接所需的權限](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
  
