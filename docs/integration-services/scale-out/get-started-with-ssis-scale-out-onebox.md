---
title: "在單一電腦上開始使用 SSIS Scale Out| Microsoft Docs"
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
ms.openlocfilehash: 8514cd548b003a39bf198b83b6b80d775a55384b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="get-started-with-integration-services-ssis-scale-out-on-a-single-computer"></a>在單一電腦上開始使用 Integration Services (SSIS) Scale Out
本節提供在 Onebox 環境中使用預設值設定 Integration Services Scale Out 的指引。

## <a name="1-install-sql-server-features"></a>1.安裝 SQL Server 的功能
在 [SQL Server 安裝精靈] 中，選取 [特徵選取] 頁面上的 [Database Engine Services]、[Integration Services]、[Scale Out Master] 和 [Scale Out Worker]。

![特徵選取 Onebox 1](media/feature-select-onebox1.PNG)

![特徵選取 Onebox 2](media/feature-select-onebox2.PNG)

在 [伺服器組態] 頁面上，按一下 [下一步] 即可使用預設服務帳戶和啟動類型。

在 [資料庫引擎組態] 頁面上，選取 [混合模式]，然後按一下 [加入目前使用者] 按鈕。 

![引擎組態](media/engine-config.PNG)

在 [Integration Services Scale Out 組態 - Master 節點] 和 [Integration Services Scale Out 組態 - Worker 節點] 頁面上，按一下 [下一步] 即可套用預設的連接埠和憑證設定。

結束 [SQL Server 安裝精靈]。

## <a name="2-install-sql-server-management-studio"></a>2.安裝 SQL Server Management Studio

[下載](../../ssms/download-sql-server-management-studio-ssms.md) SQL Server Management Studio 並進行安裝。

## <a name="3-enable-scale-out"></a>3.啟用 Scale Out
開啟 SSMS 並連接到本機 SQL Server 執行個體。
以滑鼠右鍵按一下物件總管中的 [Integration Services 目錄]，並選取 [建立類別目錄]。

在 [建立類別目錄] 對話方塊中，預設會選取 [啟用此伺服器作為 SSIS Scale Out Master]。 依正常程序建立目錄。 

## <a name="4-enable-scale-out-worker"></a>4.啟用 Scale Out Worker
在 SSMS 中，以滑鼠右鍵按一下 [SSISDB] 並選取 [管理 Scale Out]。![管理 Scale Out](media/manage-scale-out.PNG)

隨即顯示 Integration Services Scale Out Manager。 您可以使用它來管理 Scale Out。 如需詳細資訊，請參閱 [Integration Services Scale Out Manager](integration-services-ssis-scale-out-manager.md)。

若要啟用 Scale Out Worker，請切換到 **Worker Manager**，並選取您想要啟用的 Worker。 Worker 原本為停用狀態。 按一下 [啟用 Worker] 加以啟用。

## <a name="5-run-packages-in-scale-out"></a>5.在相應放大中執行套件
現在，您已準備好要在 Scale Out 中執行 SSIS 套件。請參閱[執行 Integration Services (SSIS) Scale Out 中的套件](run-packages-in-integration-services-ssis-scale-out.md)。


若要新增更多 Scale Out Worker，請參閱[使用 Scale Out Manager 新增 Scale Out Worker](add-scale-out-worker.md)。
