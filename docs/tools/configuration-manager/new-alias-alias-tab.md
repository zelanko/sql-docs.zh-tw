---
title: "新增別名 (別名索引標籤) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 785eb6fb-f67e-449d-b1c8-c38dfbb95ef6
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# 新增別名 (別名索引標籤)
  別名是可用於進行連接的替代名稱。 別名會封裝連接字串的必要元素，並以使用者選擇的名稱來公開這些元素。 您可以使用 [別名 - 新增] 對話方塊的 [別名] 頁面來指定別名的連接字串元素。 若要變更現有別名的連接字串，請參閱 [&#60;Alias&#62; 屬性 &#40;別名索引標籤&#41;](../../tools/configuration-manager/alias-properties-alias-tab.md)。  
  
 您不必填滿所有 **[內容]** 方格內的值。 有效的組合視選取的通訊協定而異。 如需有效組合的範例，請參閱下列主題。  
  
 **別名名稱**  
 您想要用來代表這個連接的名稱 (別名)。  
  
 **管道名稱** / **連接埠號碼**  
 連接字串的其他元素。 這個方塊的名稱會隨著選取的通訊協定變化。  
  
 **通訊協定**  
 用於連接的通訊協定。  
  
 **Server**  
 要連接之目標 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。  
  
## 使用別名的時機  
 依預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用**共用記憶體**通訊協定來連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本機執行個體；使用 **TCP/IP** 或**具名管道**來連接到其他電腦上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 當您想要使用 TCP/IP 或具名管道，並且想要提供自訂連接字串，或當您想要使用其他名稱 (而不使用伺服器名稱) 來進行連接時，請建立別名。  
  
### 範例  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並非接聽預設 TCP/IP 通訊埠 1433，因此您必須為連接字串提供其他連接埠號碼。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並非接聽預設具名管道，因此您必須為連接字串提供其他管道名稱。  
  
-   應用程式想要連接到伺服器上的 `ACCT`資料庫，但該資料庫已被合併為 `ACCT` 伺服器上的 `CENTRAL`執行個體。 該應用程式無法輕易修改。 您可以建立名為 `ACCT`的別名，其連接字串指向 `CENTRAL\ACCT`。  
  
## 建立有效的連接字串  
 如需有效別名屬性組合的範例描述，請參閱下列主題：  
  
-   [使用共用記憶體通訊協定建立有效的連接字串](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
-   [Creating a Valid Connection String Using TCP IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)  
  
-   [使用具名管道建立有效的連接字串](../Topic/Creating%20a%20Valid%20Connection%20String%20Using%20Named%20Pipes.md)  
  
  