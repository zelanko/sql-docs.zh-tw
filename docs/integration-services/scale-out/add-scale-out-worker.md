---
title: "使用 Scale Out Manager 加入 SSIS Scale Out Worker | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ef11448d03bd188aaea425225312af9f681f530c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="add-a-scale-out-worker-with-scale-out-manager"></a>使用 Scale Out Manager 加入 Scale Out Worker

Integration Services Scale Out Manager 可大幅降低將 Scale Out Worker 加入您現有 Scale Out 環境的複雜度。 

下列步驟可讓您將 Scale Out Worker 加入您的 Scale Out 拓撲：

## <a name="1-install-scale-out-worker"></a>1.安裝 Scale Out Worker
在 [SQL Server 安裝精靈] 中，選取 [特徵選取] 頁面上的 [Integration Services] 和 [Scale Out Worker]。 
![特徵選取背景工作](media/feature-select-worker.PNG)

在 [Integration Services Scale Out 組態 - 背景工作節點] 頁面上，您可以直接按一下 [下一步] 略過這裡的組態，並在安裝後使用 [Scale Out Manager] 來進行組態。

完成安裝精靈。

## <a name="2-open-firewall-on-scale-out-master-computer"></a>2.開啟 Scale Out Master 電腦上的防火牆
使用 Scale Out Master 電腦上的 Windows 防火牆，開啟 Scale Out Master 安裝期間所指定的連接埠 (預設為 8391)，以及 SQL Server 的連接埠 (預設為 1433)。

## <a name="3-add-scale-out-worker-with-scale-out-manager"></a>3.使用 Scale Out Manager 加入 Scale Out Worker
以系統管理員身分執行 SQL Server Management Studio，並連接到 Scale Out Master 的 SQL Server 執行個體。

以滑鼠右鍵按一下 [物件總管] 中的 [SSISDB]，然後選取 [管理 Scale Out...]。 

![管理 Scale Out](media/manage-scale-out.PNG)

在快顯的 [Scale Out Manager] 中，切換至 [背景工作管理員]。 按一下 "+" 按鈕，然後依照 [Connect Worker (連接背景工作角色)] 對話方塊上的指示進行。 如需詳細資料，請參閱 [Scale Out Manager](integration-services-ssis-scale-out-manager.md)。
