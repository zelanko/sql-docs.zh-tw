---
title: 叢集網路設定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- cluster network selection, Setup
- cluster network selection
ms.assetid: 579482ef-a023-45b2-9176-b4a4188adf9d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 48dca8e9ce522f2520521441b2e7eea349ff099b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66096440"
---
# <a name="cluster-network-configuration"></a>叢集網路組態
  使用 **[叢集網路選取]** 頁面，即可指定容錯移轉叢集執行個體的網路資源。  
  
## <a name="options"></a>選項。  
 **容錯移轉叢集網路名稱-這是用來在網路上識別容錯移轉叢集實例的名稱。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **  
  
 **網路設定**-指定容錯移轉叢集實例的 ip 類型和 ip 位址。  
  
 在加入節點和移除節點作業期間， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集之現有 IP 位址的唯讀清單。  
  
-   整合式安裝：  
  
    -   如果您要加入支援一組完全相同網路子網路的節點，而且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集的現有節點支援這組子網路，就無法加入其他 IP 位址。 相依性設定會維持不變。  
  
    -   如果您要加入支援子網路子集的節點，而且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集的現有節點支援這個子集，就無法加入其他 IP 位址資源。 IP 位址資源相依性會設定為 OR，以便反映所有指定的 IP 位址在所有叢集節點上都無效。  
  
    -   如果您要加入支援其他子網路 (除了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集之現有節點已經支援的子網路以外) 的節點，就可以選擇加入新的有效 IP 位址。 如果指定了新的 IP 位址，IP 位址資源相依性會設定為 OR，以便反映所有指定的 IP 位址在所有叢集節點上都無效。  
  
    -   如果您要加入支援其他網路子網路的節點，但是這個節點不支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集之現有節點所支援的任何子網路，就必須加入其他 IP 位址。 IP 位址資源相依性會設定為 OR，以便反映所有指定的 IP 位址在所有叢集節點上都無效。  
  
-   進階安裝：在安裝的完成步驟期間，請針對容錯移轉叢集執行個體的所有節點和子網路指定 IP 位址。 您可以針對多重子網路容錯移轉叢集指定多個 IP 位址，但是每個子網路只支援一個 IP 位址。 每個備妥的節點都至少應該是一個 IP 位址的擁有者。 如果您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集具有多個子網路，系統就會提示您將 IP 位址資源相依性設為 OR。移除節點：  
  
    -   如果所有其餘節點都支援其餘 IP 位址，系統就會提示您將 IP 位址資源相依性設定為 AND。  
  
    -   如果所有其餘節點不支援其餘 IP 位址，IP 位址資源相依性就會維持 OR。  
  
  
