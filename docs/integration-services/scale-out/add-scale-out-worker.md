---
title: "加入 SSIS 向外的延展背景工作與向外延展 Manager |Microsoft 文件"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b769236330941a107865a0b133961bce5bf6b85b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="add-a-scale-out-worker-with-scale-out-manager"></a>加入向外的延展背景工作與 擴充管理員

Integration Services 標尺出管理員大幅減輕的複雜性加入至現有的標尺出環境的標尺出背景工作。 

下列步驟可讓您將標尺出背景工作加入至向外延展拓撲：

## <a name="1-install-scale-out-worker"></a>1.安裝向外延展背景工作
在 SQL Server 安裝精靈中，選取上的 Integration Services 和標尺出背景工作**特徵選取**頁面。 
![特徵選取背景工作](media/feature-select-worker.PNG)

在**Integration Services 標尺出組態-背景工作節點** 頁面上，您只需按一下 「 下一步 以略過此設定，並使用**標尺出管理員**執行安裝後的設定。

完成安裝精靈。

## <a name="2-open-firewall-on-scale-out-master-computer"></a>2.標尺出主要電腦上開啟防火牆
開啟在標尺出主要安裝 (依預設 8391) 和連接埠的 SQL Server (1433，依預設)，指定的連接埠使用標尺出主要電腦上的 Windows 防火牆。

## <a name="3-add-scale-out-worker-with-scale-out-manager"></a>3.加入向外的延展背景工作與 擴充管理員
系統管理員身分執行 SQL Server Management Studio 並連接到標尺出主要 SQL Server 執行個體。

以滑鼠右鍵按一下**SSISDB**中 [物件總管] 並選取**管理向外...**. 

![管理向外延展](media/manage-scale-out.PNG)

在推出向上**標尺出管理員**，切換至**背景工作管理員**。 按一下"+"按鈕，並依照連接的背景工作 對話方塊上的指示。 如需詳細資訊，請參閱[標尺出管理員](integration-services-ssis-scale-out-manager.md)。

