---
title: 使用設定檔安裝 Distributed Replay |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3259232c-6963-4c9c-9d10-ae42aa262eef
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c9db8127a9a43478d891d5955190bd594fb6647b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66094579"
---
# <a name="install-distributed-replay-using-a-configuration-file"></a>使用組態檔安裝 Distributed Replay
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式可讓您根據使用者輸入和系統預設值產生組態檔。 如指定要安裝管理工具，即可使用組態檔部署管理工具、Distributed Replay Controller 及 Distributed Replay Client 三項 Distributed Replay 元件。 這個組態檔支援安裝、修復和解除安裝 Distributed Replay 元件。  
  
 安裝程式僅支援透過命令列使用組態檔。 使用組態檔時，參數的處理順序如下所述：  
  
-   組態檔會覆寫封裝中的預設值  
  
-   命令列的值會覆寫組態檔中的值  
  
 如需如何使用設定檔的詳細資訊，請參閱[使用設定檔安裝 SQL Server 2014](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md)。  
  
> [!IMPORTANT]  
>  安裝 Distributed Replay 之後，您必須在控制器電腦與用戶端電腦上建立防火牆規則，並為目標伺服器上的每個用戶端電腦授與權限。 如需詳細資訊，請參閱 [完成安裝後步驟](../../tools/distributed-replay/complete-the-post-installation-steps.md)。  
  
### <a name="to-generate-a-configuration-file"></a>若要產生組態檔  
  
1.  遵循安裝精靈的指示，直到 [準備安裝]**** 頁面。 組態檔的路徑已指定於 **[準備安裝]** 頁面的 [組態檔路徑] 區段中。  
  
2.  取消安裝程式而不實際完成安裝，即可產生 INI 檔案。  
  
### <a name="to-install-distributed-replay-using-the-configuration-file"></a>使用組態檔安裝 Distributed Replay  
  
-   透過命令提示字元執行安裝，並且使用 ConfigurationFile 參數來提供 ConfigurationFile.ini。  
  
 **範例語法**  
  
 下面是有關如何在命令提示字元中指定組態檔的範例：  
  
```  
Setup.exe /CTLRSVCPASSWORD="ctlrsvcpswd" /CLTSVCPASSWORD="cltsvcpswd" / ConfigurationFile=ConfigurationFile.INI\  
```  
  
> [!NOTE]  
>  您必須在命令列中指定這兩個密碼，因為您無法在組態檔中設定它們。  
  
  
