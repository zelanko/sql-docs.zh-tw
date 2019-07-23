---
title: SQL Server Integration Services (SSIS) Scale Out | Microsoft Docs
description: 本文提供 SQL Server Integration Services (SSIS) 相應放大功能的概觀，此功能可高效能執行 SSIS 套件
ms.custom: performance
ms.date: 12/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
author: janinezhang
ms.author: janinez
ms.openlocfilehash: abdb0350e90e1e9d1907db0405f696862434390e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897942"
---
# <a name="integration-services-ssis-scale-out"></a>Integration Services (SSIS) 相應放大

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


SQL Server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS) Scale Out 透過將套件執行散佈到多部電腦，來提供 SSIS 套件的高效能執行。 設定 Scale Out 之後，您可以從 SQL Server Management Studio (SSMS)，透過相應放大模式來平行執行多個套件執行。

## <a name="components"></a>Components
[!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out 包含一個 [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out Master 及一或多個 [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out Worker。

-   相應放大主機負責相應放大管理，以及接收來自使用者的套件執行要求。 如需詳細資訊，請參閱 [Scale Out Master](integration-services-ssis-scale-out-master.md)。

-   Scale Out Worker 會從 Scale Out Master 提取執行工作，並執行套件。 如需詳細資訊，請參閱 [Scale Out Worker](integration-services-ssis-scale-out-worker.md)。

## <a name="configuration-options"></a>設定選項
您可以在下列設定中設定 Scale Out：

-   **在單一電腦上**，其中，Scale Out Master 和 Scale Out Worker 是在同一部電腦上並排執行。

-   **在多部電腦上**其中，每個 Scale Out Worker 都在不同的電腦上。

## <a name="what-you-can-do"></a>您可以採取的方法
設定 Scale Out 之後，您可以執行下列動作：

-   平行執行多個部署至 SSISDB 目錄的套件。 如需詳細資訊，請參閱 [在 Scale Out 中執行套件](run-packages-in-integration-services-ssis-scale-out.md)。

-   管理 Scale Out Manager 應用程式中的 Scale Out 拓撲。 如需詳細資訊，請參閱 [Integration Services Scale Out Manager](integration-services-ssis-scale-out-manager.md)。

## <a name="next-steps"></a>後續步驟
-   [在單一電腦上開始使用 Integration Services (SSIS) Scale Out](get-started-with-ssis-scale-out-onebox.md)

-   [逐步解說：設定整合服務 Scale Out](walkthrough-set-up-integration-services-scale-out.md)
