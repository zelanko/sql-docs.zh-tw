---
title: 連線到 SQL Server 進行刪除 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 030b10c2-6b88-4c2c-bf67-22994be25a60
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0b7c3b34f60f69a788c67022151dd90ddc9235e8
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52779950"
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
  
-   **SQL Server 驗證**:如果您選取此選項時，您必須輸入**登入**並**密碼**中的使用者[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您要連接到。  
  
 **選項。**  
 按一下箭頭即可檢視要設定的可用選項。 您可以選擇保留這些選項的預設值。 可用的選項如下：  
  
-   **連接逾時**:輸入的時間 （以秒為單位） 的程式等候的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]產生逾時錯誤之前建立的連線。 預設值為 **15**。  
  
-   **執行逾時**:輸入此程式會等候執行 SQL 命令產生逾時錯誤之前的時間 （以秒為單位）。 預設值是 **30**。  
  
-   **加密連接**:選取 **加密連接**以確保[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在建立連接已加密來保障隱私權。  
  
-   **進階**：按一下 [進階]，並在必要時，於 [進階連接屬性] 對話方塊中輸入其他任何連接屬性。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 連接所需的 CDC 服務權限](sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
  
