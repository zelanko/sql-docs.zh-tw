---
title: 瀏覽伺服器 (網路伺服器) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.browseservers.network.f1
ms.assetid: a59ffcd6-4b69-4c5c-9740-699ccb2183fb
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 0ba5e4e5dd6d9a6541a98e0cb30229d7335bac24
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936076"
---
# <a name="browse-for-servers-network-servers"></a>瀏覽伺服器 (網路伺服器)
  如果連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 元件，但不知道 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的確實名稱，請在 [伺服器名稱]**** 方塊中按一下 [瀏覽其他]****，以開啟 [瀏覽伺服器]**** 對話方塊。  
  
 伺服器電腦上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser 服務會擴展這個對話方塊。 執行個體名稱未出現在清單中的原因很多：  
  
-   在執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的電腦上可能未執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Browser 服務。  
  
-   防火牆可能封鎖了 UDP 通訊埠 1434。  
  
-   可能設定了 **HideInstance** 旗標。  
  
 若要連接至未出現在清單中的執行個體，請輸入執行個體的完整連接字串 (包括 TCP/IP 通訊埠編號或具名管道的管道名稱)。  
  
## <a name="options"></a>選項。  
 **從網路中選取一個連接的 SQL Server 執行個體**  
 按一下樹狀結構中所顯示的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，以指定您想要連接到的伺服器。 您可以按一下以或符號標示的節點，以顯示或隱藏部分樹狀檢視 **+** **-** 。  
  
  
