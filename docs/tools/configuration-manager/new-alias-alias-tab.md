---
title: "新增別名 （別名索引標籤） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 785eb6fb-f67e-449d-b1c8-c38dfbb95ef6
caps.latest.revision: "21"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e721666582366b9c9f141723e7f4d6f14fbe4552
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="new-alias-alias-tab"></a>新增別名 (別名索引標籤)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]別名是可用於進行連接的替代名稱。 別名會封裝連接字串的必要元素，並以使用者選擇的名稱來公開這些元素。 您可以使用 [別名 - 新增] 對話方塊的 [別名] 頁面來指定別名的連接字串元素。 若要變更現有別名的連接字串，請參閱 [&#60;Alias&#62; 屬性 &#40;別名索引標籤&#41;](../../tools/configuration-manager/alias-properties-alias-tab.md)。  
  
 您不必填滿所有 **[內容]** 方格內的值。 有效的組合視選取的通訊協定而異。 如需有效組合的範例，請參閱下列主題。  
  
 **別名名稱**  
 您想要用來代表這個連接的名稱 (別名)。  
  
 **管道名稱** / **連接埠號碼**  
 連接字串的其他元素。 這個方塊的名稱會隨著選取的通訊協定變化。  
  
 **通訊協定**  
 用於連接的通訊協定。  
  
 **Server**  
 要連接之目標 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。  
  
## <a name="when-to-use-an-alias"></a>使用別名的時機  
 依預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共用記憶體 **通訊協定來連接到** 的本機執行個體；使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] TCP/IP **或** 具名管道 **來連接到其他電腦上的**執行個體。 當您想要使用 TCP/IP 或具名管道，並且想要提供自訂連接字串，或當您想要使用其他名稱 (而不使用伺服器名稱) 來進行連接時，請建立別名。  
  
### <a name="examples"></a>範例  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並非接聽預設 TCP/IP 通訊埠 1433，因此您必須為連接字串提供其他連接埠號碼。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並非接聽預設具名管道，因此您必須為連接字串提供其他管道名稱。  
  
-   應用程式想要連接到伺服器上的 `ACCT`資料庫，但該資料庫已被合併為 `ACCT` 伺服器上的 `CENTRAL`執行個體。 該應用程式無法輕易修改。 您可以建立名為 `ACCT`的別名，其連接字串指向 `CENTRAL\ACCT`。  
  
## <a name="creating-a-valid-connection-string"></a>建立有效的連接字串  
 如需有效別名屬性組合的範例描述，請參閱下列主題：  
  
-   [使用共用記憶體通訊協定建立有效的連接字串](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
-   [Creating a Valid Connection String Using TCP IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)  
  
-   [使用具名管道建立有效的連接字串](http://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)  
  
  
