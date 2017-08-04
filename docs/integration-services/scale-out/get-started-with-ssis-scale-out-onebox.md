---
title: "開始使用 SSIS 小數位數，在單一電腦上編寫 |Microsoft 文件"
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
ms.openlocfilehash: 7175c63be4c0e15e50f2020f75d283ac0e3dfdbf
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="get-started-with-integration-services-ssis-scale-out-on-a-single-computer"></a>開始使用 Integration Services (SSIS) 向外在單一電腦上
本節提供設定預設設定的其中一個方塊環境中的 [Integration Services 向外的指引。

## <a name="1-install-sql-server-features"></a>1.安裝 SQL Server 功能
在 SQL Server 安裝精靈中，選取 Database Engine Services、 Integration Services、 標尺出主要和標尺出背景工作上**特徵選取**頁面。

![功能選取 Onebox 1](media/feature-select-onebox1.PNG)

![功能選取 Onebox 2](media/feature-select-onebox2.PNG)

在**伺服器組態**頁面上，只要按一下 [下一步 」 會使用預設服務帳戶和啟動類型。

上**資料庫引擎組態**頁面上，選取 「**混合模式**"和按一下"**加入目前使用者**」 按鈕。 

![引擎組態](media/engine-config.PNG)

一個**Integration Services 標尺出組態的主要節點**和**Integration Services 標尺出組態-背景工作節點**頁面，只要按一下 [下一步 」 套用預設的連接埠和憑證的設定。

完成 SQL Server 安裝精靈。

## <a name="2-install-sql-server-management-studio"></a>2.安裝 SQL Server Management Studio

[下載](../../ssms/download-sql-server-management-studio-ssms.md)SQL Server Management Studio 並安裝它。

## <a name="3-enable-scale-out"></a>3.啟用向外延展
開啟 SSMS 並連接到本機 Sql Server 執行個體。
以滑鼠右鍵按一下**Integration Services 目錄**中 [物件總管] 並選取**建立類別目錄**。

在**建立類別目錄**] 對話方塊中，**啟用此伺服器為主要的 SSIS 擴充**預設會選取。 就像往常一樣建立目錄。 

## <a name="4-enable-scale-out-worker"></a>4.啟用向外延展背景工作
在 SSMS 中，以滑鼠右鍵按一下**SSISDB**選取**管理向外...**. 
![管理向外延展](media/manage-scale-out.PNG)

Integration Services 標尺出管理員就會出現。 您可以向外管理它。 如需詳細資訊，請參閱[Integration Services 標尺出管理員](integration-services-ssis-scale-out-manager.md)。

若要啟用標尺出背景工作，請切換到**背景工作管理員**並選取您想要啟用的背景工作。 原先已停用背景工作。 按一下**啟用工作者**加以啟用。

## <a name="5-run-packages-in-scale-out"></a>5.在相應放大中執行套件
現在，您就準備好要執行 SSIS 封裝在向外。 請參閱[Integration Services (SSIS) 中的執行的封裝向外延展](run-packages-in-integration-services-ssis-scale-out.md)。


若要新增更多的標尺出背景工作，請參閱[加入標尺出背景工作與標尺出 Manager](add-scale-out-worker.md)。
