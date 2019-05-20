---
title: 使用 Scale Out Manager 加入 SSIS Scale Out Worker | Microsoft Docs
description: 本文描述如何使用 Scale Out Manager 將 SSIS Scale Out Worker 新增至現有的 Scale Out 環境。
ms.custom: performance
ms.date: 12/19/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
manager: craigg
ms.openlocfilehash: 5375f3992cd5d969276b02612f02ab4c32842689
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65718780"
---
# <a name="add-a-scale-out-worker-with-scale-out-manager"></a>使用 Scale Out Manager 加入 Scale Out Worker

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Integration Services Scale Out Manager 可簡化將 Scale Out Worker 新增至現有 Scale Out 環境的過程。 

遵循下列步驟，將 Scale Out Worker 新增至 Scale Out 拓撲：

## <a name="1-install-scale-out-worker"></a>1.安裝 Scale Out Worker
在 [SQL Server 安裝精靈] 中，選取 [特徵選取] 頁面上的 [Integration Services] 和 [Scale Out Worker]。 
![特徵選取背景工作](media/feature-select-worker.PNG)

在 [Integration Services 相應放大設定 - 背景工作節點] 頁面上，您目前可以按一下 [下一步] 略過設定，並在安裝之後使用 [Scale Out Manager] 來執行設定。

完成安裝精靈。

## <a name="2-open-the-firewall-on-the-scale-out-master-computer"></a>2.開啟 Scale Out Master 電腦上的防火牆
在 Scale Out Master 電腦的 Windows 防火牆中，開啟 Scale Out Master 安裝期間所指定的連接埠 (預設為 8391)，以及 SQL Server 的連接埠 (預設為 1433)。

## <a name="3-add-a-scale-out-worker-with-scale-out-manager"></a>3.使用 Scale Out Manager 加入 Scale Out Worker
以系統管理員身分執行 SQL Server Management Studio，並連接到 Scale Out Master 的 SQL Server 執行個體。

在物件總管中，以滑鼠右鍵按一下 [SSISDB]，然後選取 [管理相應放大]。 

![管理 Scale Out](media/manage-scale-out.PNG)

在 [Scale Out Manager] 對話方塊中，切換至 [背景工作管理員]。 選取 **+**，然後遵循 [Connect Worker (連線背景工作)] 對話方塊中的指示進行。 

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱 [Scale Out Manager](integration-services-ssis-scale-out-manager.md)。
