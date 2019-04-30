---
title: Distributed Replay Client 組態 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: ccf03e32-6bd9-43c0-b9b6-9fe0d9163339
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e8b179d54ff39ffbb67193f88cd192aac6992d7d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63253615"
---
# <a name="distributed-replay-client-configuration"></a>Distributed Replay Client 組態
  您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈的 [Distributed Replay Client 組態] 頁面來指定您想要授與 Distributed Replay Client 服務之管理權限的使用者。  
  
 擁有管理權限的使用者將可不受限制地存取 Distributed Replay Client 服務。  
  
## <a name="options"></a>選項。  
 **控制器名稱**  
 這是選擇性參數，而且預設值是\<*空白*>。  
  
 針對 Distributed Replay Client 服務，輸入將與用戶端電腦進行通訊之控制器的名稱。 請注意下列事項：  
  
-   名稱必須是完整網域名稱 (FQDN)。 例如，Microsoft 的產品階層中稱為 server1 的主機，其 FQDN 會是 server1.products.microsoft.com。  
  
-   如果您已經設定了控制器，請在設定每個用戶端時輸入該控制器的名稱。  
  
-   如果您尚未設定控制器，則可以將控制器名稱留空。 不過，您必須在 [用戶端組態]  檔中，手動輸入控制器名稱。  
  
 **工作目錄**  
 指定 Distributed Replay Client 服務的工作目錄。  
  
 預設工作目錄為 \<磁碟機代號>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\。  
  
 **結果目錄**  
 指定 Distributed Replay Client 服務的結果目錄。  
  
 預設工作目錄為 \<磁碟機代號>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\。  
  
  
