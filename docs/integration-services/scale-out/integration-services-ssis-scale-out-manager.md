---
title: "SQL Server Integration Services Scale Out 管理員 | Microsoft Docs"
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
ms.openlocfilehash: 84fe58d4dc7894728c43cb19d17d3444b5b84820
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="integration-services-scale-out-manager"></a>Integration Services Scale Out 管理員

Scale Out 管理員是可讓您在單一位置管理完整 SSIS Scale Out 拓撲的管理工具。 它可消除在多部電腦上運作及處理 TSQL 命令的負擔。 

有兩種方式可用來觸發 Scale Out 管理員。

## <a name="1-open-scale-out-manager-from-sql-server-management-studio"></a>1.從 SQL Server Management Studio 中開啟 Scale Out 管理員
開啟 SQL Server Management Studio，並連線至 Scale Out 主機的 SQL Server 執行個體。

以滑鼠右鍵按一下 [物件總管] 中的 [SSISDB]，並選取 [管理向外延展...]。![管理向外延展](media/manage-scale-out.PNG)

> [!NOTE]
> 建議以系統管理員身分執行 SQL Server Management Studio，因為一些 Scale Out 管理作業 (例如「新增 Scale Out 背景工作」) 需要系統管理權限。


## <a name="2-open-scale-out-manager-by-runing-ismanagerexe-directly"></a>2.直接執行 ISManager.exe 開啟 Scale Out 管理員

ISManager.exe 位於 %SystemDrive%\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn\Management 之下。 以滑鼠右鍵按一下 **ISManager.exe**，然後選取 [以系統管理員身分執行]。 

在其開啟之後，您需要輸入 Scale Out 主機的 SQL Server 名稱並進行連線，才能管理您的 Scale Out。

![入口網站連線](media/portal-connect.PNG)

Scale Out 管理員可提供各種功能，如下所示。 

## <a name="enable-scale-out"></a>啟用 Scale Out
連線至 SQL Server 之後，如果未啟用 Scale Out，您可以按一下 [啟用] 按鈕來啟用它。

![入口網站的啟用 Scale Out](media/portal-enable-scale-out.PNG) 
## <a name="view-scale-out-master-status"></a>檢視 Scale Out 主機狀態
Scale Out 主機的狀態會顯示在 [儀表板] 頁面。

![入口網站的儀表板](media/portal-dashboard.PNG)
## <a name="view-scale-out-worker-status"></a>檢視 Scale Out 背景工作狀態
Scale Out 背景工作的狀態會顯示在 [背景工作管理員] 頁面。 您可以按一下每個背景工作，以查看個別的狀態。

![入口網站的背景工作管理員](media/portal-worker-manager.PNG)

## <a name="add-scale-out-worker"></a>新增 Scale Out 背景工作
若要新增 Scale Out 背景工作，請按一下 Scale Out 背景工作清單底部的 "+" 按鈕。 

輸入您想要新增的 Scale Out 背景工作的電腦名稱，然後按一下 [驗證]。 Scale Out 管理員會檢查目前的使用者是否有權存取 Scale Out 主機和 Scale Out 背景工作電腦上的憑證存放區。

![連線背景工作](media/connect-worker.PNG)

如果通過驗證，Scale Out 管理員將嘗試讀取您的背景工作設定檔，並取得背景工作的憑證指紋。 如需詳細資訊，請參閱 [Scale Out 背景工作](integration-services-ssis-scale-out-worker.md)。 如果無法讀取背景工作設定檔，有兩種替代方式可為您提供背景工作憑證。 

您可以直接輸入背景工作憑證的指紋 

![背景工作憑證 1](media/portal-cert1.PNG)

或提供憑證檔案。 

![背景工作憑證 2](media/portal-cert2.PNG)

收集所有資訊之後，Scale Out 管理員將提供要執行的動作。 它通常包含安裝憑證、更新背景工作設定檔和重新啟動背景工作服務。 

![入口網站的新增確認 1](media/portal-add-confirm1.PNG)

如果背景工作憑證無法存取，您需要自行手動加以更新並重新啟動背景工作服務。

![入口網站的新增確認 2](media/portal-add-confirm2.PNG)

按一下 [確認] 核取方塊，然後開始新增 Scale Out 背景工作。

## <a name="delete-scale-out-worker"></a>刪除 Scale Out 背景工作
若要刪除 Scale Out 背景工作，請選取 Scale Out 背景工作，然後按一下 Scale Out 背景工作清單底部的 "-" 的按鈕。


## <a name="enabledisable-scale-out"></a>啟用/停用 Scale Out
若要啟用或停用 Scale Out 背景工作，請選取 Scale Out 背景工作，然後按一下 [啟用背景工作] 或 [停用背景工作] 按鈕。 如果背景工作未離線，Scale Out 管理員的背景工作狀態也會隨之變更。

## <a name="edit-scale-out-worker-description"></a>編輯 Scale Out 背景工作的描述
若要編輯 Scale Out 背景工作的描述，請選取 Scale Out 背景工作，然後按一下 [編輯] 按鈕。 在您完成編輯之後，按一下 [儲存] 按鈕。

![入口網站的儲存背景工作](media/portal-save-worker.PNG)

