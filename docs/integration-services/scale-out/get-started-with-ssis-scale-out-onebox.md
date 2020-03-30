---
title: 在單一電腦上開始使用 SSIS Scale Out| Microsoft Docs
description: 本文說明您在單一電腦上開始使用 SSIS Scale Out 所需了解的一切項目
ms.custom: performance
ms.date: 12/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: maghan
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: a2d6929277b7d024e45daaefd5cb41dccd495c63
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68082157"
---
# <a name="get-started-with-integration-services-ssis-scale-out-on-a-single-computer"></a>在單一電腦上開始使用 Integration Services (SSIS) Scale Out

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


本節提供在單一電腦環境中使用預設設定來設定 Integration Services Scale Out 的指引。

## <a name="1-install-sql-server-features"></a>1.安裝 SQL Server 的功能
在 [SQL Server 安裝精靈] 中，於 [特徵選取]  頁面上選取下列項目：
-   Database Engine 服務
-   Integration Services
    -   Scale Out Master
    -   Scale Out Worker

![特徵選取前半清單](media/feature-select-onebox1.PNG)

![特徵選取後半清單](media/feature-select-onebox2.PNG)

在 [伺服器設定]  頁面上，按一下 [下一步]  接受預設服務帳戶和啟動類型。

在 [資料庫引擎設定]  頁面上，選取 [混合模式]  ，然後按一下 [新增目前使用者]  。 

![引擎組態](media/engine-config.PNG)

在 [Integration Services 擴增設定 - 主要節點]  和 [Integration Services 擴增設定 - 背景工作節點]  頁面上，按一下 [下一步]  接受連接埠和憑證的預設設定。

結束 [SQL Server 安裝精靈]。

## <a name="2-install-sql-server-management-studio"></a>2.安裝 SQL Server Management Studio

下載並安裝 [SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md)。

## <a name="3-enable-scale-out"></a>3.啟用 Scale Out
開啟 SSMS 並連接到本機 SQL Server 執行個體。
在物件總管中，以滑鼠右鍵按一下 [Integration Services 目錄]  ，然後選取 [建立目錄]  。

在 [建立目錄]  對話方塊中，預設會選取 [啟用此伺服器作為 SSIS 擴增主機]  。

## <a name="4-enable-a-scale-out-worker"></a>4.啟用 Scale Out Worker
在 SSMS 中，以滑鼠右鍵按一下 [SSISDB]  ，然後選取 [管理擴增]  。 

![管理 Scale Out](media/manage-scale-out.PNG)

隨即開啟 Integration Services Scale Out Manager 應用程式。 如需詳細資訊，請參閱 [Scale Out Manager](integration-services-ssis-scale-out-manager.md)。

若要啟用 Scale Out Worker，請切換至 [背景工作管理員]  ，並選取您想要啟用的背景工作。 預設會停用背景工作。 按一下 [啟用背景工作]  以啟用選取的背景工作。

## <a name="5-run-packages-in-scale-out"></a>5.在擴增中執行套件
現在，您已準備好要在 Scale Out 中執行 SSIS 套件。如需詳細資訊，請參閱[在 Integration Services (SSIS) Scale Out 中執行套件](run-packages-in-integration-services-ssis-scale-out.md)。

## <a name="next-steps"></a>後續步驟
-   [使用 Scale Out Manager 新增 Scale Out Worker](add-scale-out-worker.md)。
