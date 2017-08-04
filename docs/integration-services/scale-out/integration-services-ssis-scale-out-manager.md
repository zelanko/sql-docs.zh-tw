---
title: "SQL Server Integration Services 向外延展 Manager |Microsoft 文件"
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
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 96748296acd1b2f5ba98558335fece9637eadb87
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-scale-out-manager"></a>Integration Services 擴充管理員

標尺出管理員是可讓您管理完整 SSIS 向外的拓撲在單一位置管理工具。 它會移除多部電腦上運作，而 TSQL 命令的處理的負擔。 

有兩種方式，來觸發管理員出小數位數。

## <a name="1-open-scale-out-manager-from-sql-server-management-studio"></a>1.從 SQL Server Management Studio 中開啟 擴充管理員
開啟 SQL Server Management Studio 並連接到標尺出主要 SQL Server 執行個體。

以滑鼠右鍵按一下**SSISDB**中 [物件總管] 並選取**管理向外...**. 
![管理向外延展](media/manage-scale-out.PNG)

> [!NOTE]
> 建議為一些向外管理作業，例如 「 新增的範圍外背景工作 」 的系統管理員身分執行 SQL Server Management Studio 將需要系統管理權限。


## <a name="2-open-scale-out-manager-by-runing-ismanagerexe-directly"></a>2.直接執行下列項目的 ISManager.exe 開啟標尺出管理員

ISManager.exe 找出 %SystemDrive%\Program 檔案 (x86) \Microsoft SQL Server\140\DTS\Binn\Management 底下。 以滑鼠右鍵按一下**ISManager.exe**並選取 [以系統管理員身分執行]。 

它會開啟之後，您需要輸入的小數位數出主要 Sql Server 名稱和連接到它，才能管理您向外。

![入口網站連接](media/portal-connect.PNG)

標尺出管理員會提供各種功能，如下所示。 

## <a name="enable-scale-out"></a>啟用向外延展
連接到 SQL Server 之後，如果未啟用向外，您可以按一下 [啟用] 按鈕，來啟用它。

![入口網站啟用向外延展](media/portal-enable-scale-out.PNG) 
## <a name="view-scale-out-master-status"></a>檢視標尺出主要狀態
標尺出主機的狀態會顯示在**儀表板**頁面。

![入口網站儀表板](media/portal-dashboard.PNG)
## <a name="view-scale-out-worker-status"></a>檢視標尺出背景工作狀態
標尺出背景工作的狀態會顯示在**背景工作管理員**頁面。 您可以按一下每個背景工作，以了解個別的狀態。

![入口網站背景工作管理員](media/portal-worker-manager.PNG)

## <a name="add-scale-out-worker"></a>加入向外延展背景工作
若要加入標尺出背景工作，按一下"+"按鈕在標尺出背景工作清單的底部。 

輸入您想要新增，然後按一下 「 驗證 」 出工作者標尺的電腦名稱。 標尺出管理員會檢查目前使用者是否有權存取，以標尺出主要和標尺出背景工作的電腦上的憑證存放區。

![連接背景工作](media/connect-worker.PNG)

如果通過驗證，標尺出管理員將嘗試讀取您的背景工作的組態檔，並取得背景工作的憑證指紋。 如需詳細資訊，請參閱[標尺出工作者](integration-services-ssis-scale-out-worker.md)。 如果您不能讀取組態檔的背景工作，有兩個替代方式，讓您提供的背景工作憑證。 

您可能可以直接輸入背景工作憑證的指紋 

![1 的背景工作憑證](media/portal-cert1.PNG)

或提供的憑證檔案。 

![背景工作憑證 2](media/portal-cert2.PNG)

收集所有資訊後, 標尺出管理員會提供要執行的動作。 Tyically，它包含安裝憑證、 背景工作組態檔更新和重新啟動服務的背景工作。 

![入口網站加入確認 1](media/portal-add-confirm1.PNG)

背景工作憑證不是可存取，您需要自行手動加以更新並重新啟動背景工作服務。

![入口網站加入確認 2](media/portal-add-confirm2.PNG)

按一下 [確認] 核取方塊，然後開始將加入標尺出背景工作。

## <a name="delete-scale-out-worker"></a>刪除向外延展背景工作
若要刪除標尺出背景工作，請選取標尺出背景工作，然後按一下 「-」 在標尺出背景工作清單底部的按鈕。


## <a name="enabledisable-scale-out"></a>啟用/停用向外延展
若要啟用或停用延展出背景工作，請選取標尺出背景工作，按一下 「 啟用背景工作 」 或 「 停用背景工作 」 按鈕。 如果背景工作未離線，也會隨著變更標尺出管理員上的背景工作狀態。

## <a name="edit-scale-out-worker-description"></a>編輯標尺出背景工作描述
若要編輯的標尺出背景工作的描述，選取標尺出背景工作，並按一下 [編輯] 按鈕。 在您完成編輯之後，按一下 [儲存] 按鈕。

![儲存背景工作的入口網站](media/portal-save-worker.PNG)


