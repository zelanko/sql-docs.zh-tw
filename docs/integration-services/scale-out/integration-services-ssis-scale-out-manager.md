---
title: SQL Server Integration Services Scale Out 管理員 | Microsoft Docs
description: 本文描述您可以用來管理 SSIS Scale Out 的 Scale Out Manager
ms.custom: performance
ms.date: 12/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: craigg
ms.openlocfilehash: 3023b3d2847e206aa5646a14aa8a5ee5eff68a9c
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35331252"
---
# <a name="integration-services-scale-out-manager"></a>Integration Services Scale Out 管理員

Scale Out Manager 是一種管理工具，可讓您透過單一應用程式管理整個 SSIS Scale Out 拓撲。 它會移除在多部電腦上執行管理工作以及執行 Transact-SQL 命令的負擔。

## <a name="open-scale-out-manager"></a>開啟 Scale Out Manager

有兩種方式可以開啟 Scale Out Manager。

### <a name="1-open-scale-out-manager-from-sql-server-management-studio"></a>1.從 SQL Server Management Studio 中開啟 Scale Out 管理員
開啟 SQL Server Management Studio (SSMS)，並連線至 Scale Out Master 的 SQL Server 執行個體。

在物件總管中，以滑鼠右鍵按一下 [SSISDB]，然後選取 [管理相應放大]。

![管理 Scale Out](media/manage-scale-out.PNG)

> [!NOTE]
> 建議以管理員身分執行 SSMS，因為某些 Scale Out 管理作業 (例如新增 Scale Out Worker) 需要系統管理權限。

### <a name="2-open-scale-out-manager-by-running-ismanagerexe"></a>2.執行 ISManager.exe 來開啟 Scale Out Manager

在 `%SystemDrive%\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn\Management` 下方找到 `ISManager.exe`。 以滑鼠右鍵按一下 **ISManager.exe**，然後選取 [以系統管理員​​身分執行]。 

開啟 Scale Out Manager 之後，輸入 Scale Out Master 的 SQL Server 執行個體名稱，並與其連線以管理 Scale Out 環境。

![入口網站連線](media/portal-connect.PNG)

## <a name="tasks-available-in-scale-out-manager"></a>Scale Out Manager 中可用的工作
在 Scale Out Manager 中，您可以執行下列動作：

### <a name="enable-scale-out"></a>啟用 Scale Out
連線至 SQL Server 之後，如果未啟用 Scale Out，則可以選取 [啟用] 予以啟用。

![入口網站的啟用 Scale Out](media/portal-enable-scale-out.PNG) 

### <a name="view-scale-out-master-status"></a>檢視 Scale Out 主機狀態
Scale Out 主機的狀態會顯示在 [儀表板] 頁面。

![入口網站的儀表板](media/portal-dashboard.PNG)

### <a name="view-scale-out-worker-status"></a>檢視 Scale Out 背景工作狀態
Scale Out 背景工作的狀態會顯示在 [背景工作管理員] 頁面。 您可以選取每個背景工作，以查看個別狀態。

![入口網站的背景工作管理員](media/portal-worker-manager.PNG)

### <a name="add-a-scale-out-worker"></a>新增 Scale Out Worker
若要新增 Scale Out Worker，請選取 Scale Out Worker 清單底部的 **+**。 

輸入您想要新增的 Scale Out Worker 的電腦名稱，然後按一下 [驗證]。 Scale Out Manager 會檢查目前的使用者是否有權存取 Scale Out Master 和 Scale Out Worker 電腦上的憑證存放區

![連線背景工作](media/connect-worker.PNG)

如果驗證成功，Scale Out Manager 會嘗試讀取背景工作伺服器設定檔，並取得背景工作的憑證指紋。 如需詳細資訊，請參閱 [Scale Out Worker](integration-services-ssis-scale-out-worker.md)。 如果 Scale Out Manager 無法讀取背景工作服務設定檔，則有兩種替代方式可以提供背景工作憑證。 

1.  您可以直接輸入背景工作憑證的指紋。

    ![背景工作憑證 1](media/portal-cert1.PNG)

2.  或者，您可以提供憑證檔案。 

    ![背景工作憑證 2](media/portal-cert2.PNG)

收集資訊之後，Scale Out Manager 會描述要執行的動作。 一般而言，這些動作包含安裝憑證、更新背景工作服務設定檔，以及重新啟動背景工作服務。

![入口網站的新增確認 1](media/portal-add-confirm1.PNG)

如果無法存取背景工作憑證，則您必須手動進行更新，並重新啟動背景工作服務。

![入口網站的新增確認 2](media/portal-add-confirm2.PNG)

選取 [確認] 核取方塊，然後選取 [確定] 開始新增 Scale Out Worker。

### <a name="delete-a-scale-out-worker"></a>刪除 Scale Out Worker
若要刪除 Scale Out Worker，請選取 Scale Out Worker，然後選取 Scale Out Worker 清單底部的 **-**。

### <a name="enable-or-disable-a-scale-out-worker"></a>啟用或停用 Scale Out Worker
若要啟用或停用 Scale Out Worker，請選取 Scale Out Worker，然後選取 [啟用背景工作] 或 [停用背景工作]。 如果背景工作未離線，則 Scale Out Manager 中所顯示的背景工作狀態會據此變更。

## <a name="edit-a-scale-out-worker-description"></a>編輯 Scale Out Worker 描述
若要編輯 Scale Out Worker 的描述，請選取 Scale Out Worker，然後選取 [編輯]。 在您完成描述的編輯之後，請選取 [儲存]。

![入口網站的儲存背景工作](media/portal-save-worker.PNG)

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱下列文章：
-   [Integration Services (SSIS) Scale Out Master](integration-services-ssis-scale-out-master.md)
-   [Integration Services (SSIS) Scale Out Worker](integration-services-ssis-scale-out-worker.md)