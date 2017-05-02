---
title: "瀏覽伺服器 (網路伺服器) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.browseservers.network.f1
ms.assetid: a59ffcd6-4b69-4c5c-9740-699ccb2183fb
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0dfaef0364cf72e994b0fe5de778adc8a18bd715
ms.lasthandoff: 04/11/2017

---
# <a name="browse-for-servers-network-servers"></a>瀏覽伺服器 (網路伺服器)
如果連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 元件，但不知道 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 執行個體的確實名稱，請在 [伺服器名稱]**** 方塊中按一下 [瀏覽其他]****，以開啟 [瀏覽伺服器]**** 對話方塊。  
  
伺服器電腦上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Browser 服務會擴展這個對話方塊。 執行個體名稱未出現在清單中的原因很多：  
  
-   在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 的電腦上可能未執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Browser 服務。  
  
-   防火牆可能封鎖了 UDP 通訊埠 1434。  
  
-   可能設定了 **HideInstance** 旗標。  
  
若要連接至未出現在清單中的執行個體，請輸入執行個體的完整連接字串 (包括 TCP/IP 通訊埠編號或具名管道的管道名稱)。  
  
## <a name="options"></a>選項。  
**從網路中選取一個連接的 SQL Server 執行個體**  
按一下樹狀結構中所顯示的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 執行個體，以指定您想要連接到的伺服器。 您可以按一下標示 **+** 或 **-** 符號的節點，以顯示或隱藏部分樹狀檢視。  
  

