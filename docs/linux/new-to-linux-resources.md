---
title: 不熟悉 Linux 的 SQL 使用者所適用的資源
titleSuffix: SQL Server
description: 不熟悉 Linux 的 SQL 使用者所適用的資源和指引。
author: VanMSFT
ms.author: vanto
ms.date: 08/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 789178113f1e22df2d2cf028d2f6e5f93e9b5b0e
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646818"
---
# <a name="new-to-linux-resources-for-sql-users"></a>不熟悉 Linux 的 SQL 使用者所適用的資源

本文透過介紹 Linux 概念來提供學習路徑。 使用文章中各個區段作為引導式學習路徑，以熟悉 Linux 環境。

這不是完整的學習清單，僅能提供管理和巡覽 Linux 上 SQL Server 環境的最基本需求。 如需深入了解，請參閱[完整的教學課程清單](https://www.linux.org/forums/linux-beginner-tutorials.123/)。 

## <a name="what-is-linux"></a>什麼是 Linux？

[什麼是 Linux](https://www.linux.org/threads/what-is-linux.4106/) 課程模組會介紹 Linux 作業系統的歷史。 本課程模組會說明「核心」，以及 Linux 至今為止的發展。 本教學課程的介紹可協助開始使用 Linux。 

## <a name="select-a-distribution"></a>選取發行版本

在了解 Linux 的歷史之後，請決定哪個 [Linux 發行版本](https://www.linux.org/threads/selecting-a-linux-distribution.4117/)最能符合商務需求。 Red Hat Enterprise Linux (RHEL)、SUSE Linux Enterprise Server (SLES) 及 Ubuntu 等發行版本[都支援 SQL Server](sql-server-linux-release-notes-2019.md#supported-platforms)。


## <a name="get-around-directories"></a>取得目錄

在選擇適當的 Linux 發行版本之後，請[瀏覽 Linux 目錄](https://www.linux.org/threads/getting-around-in-linux-directories.4120/)加以熟悉。

本課程模組可協助回答下列問題：

- 如何在不同的檔案之間瀏覽 
- 如何辨識目錄中的檔案
- 識別不同的目錄 


## <a name="install-new-software"></a>安裝新的軟體 

接下來，了解如何在新 Linux 作業系統上[安裝新的軟體](https://www.linux.org/threads/installing-new-software-debian-red-hat-slackware.4119/)。 本課程模組會詳細說明如何將新軟體安裝到 Debian 和 Red Hat Linux 作業系統。 


## <a name="root-versus-system-user"></a>根使用者與系統使用者

了解使用者權限，以及[根使用者與系統使用者](https://www.linux.org/threads/when-to-work-as-root-when-to-work-as-a-system-user.4136/)之間的差異。 本課程模組可協助決定哪些使用者權限適合用於哪一個案例。 

## <a name="file-system-and-permissions"></a>檔案系統與權限

當熟悉在 Linux 中辨識不同的使用者和群組之後，請學習如何使用 [chown (變更擁有權)](https://www.linux.org/threads/file-permisions-chown.4125/) 以及 [chmod (變更權限)](https://www.linux.org/threads/file-permissions-chmod.4124) 命令來變更 Linux 作業系統中不同檔案的擁有權與檔案權限。 


## <a name="commands-for-system-administration"></a>系統管理的命令

介紹系統管理員用來控制 Linux 作業系統的[常用命令](https://www.linux.org/threads/commands-for-system-administration.4126/)。 這些命令包括：`df`、`du`、`TOP`、`ps`、`mkdir`、`rmdir`、`rm` 和 `mv`。 


## <a name="next-steps"></a>後續步驟

在熟悉使用 Linux 環境之後，請參閱 Linux 上 SQL Server 的 [版本與元件](sql-server-linux-editions-and-components-2019.md) ，以及 [支援的 Linux 平台](sql-server-linux-release-notes-2019.md)。 

若要深入了解，請參閱[其他 Linux 教學課程](https://www.linux.org/forums/linux-beginner-tutorials.123/)以及[常見問題](sql-server-linux-faq.md)。
