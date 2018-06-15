---
title: SQL Server on Linux 的概觀 |Microsoft 文件
description: 本文描述 SQL Server 如何在 Linux 上執行，並提供如何了解詳細資訊。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/24/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 9dcc6a90-0add-42c2-815b-862e4e2a21ac
ms.openlocfilehash: 2c67e5d1563ef2420f45ec4b1d0093de888dd157
ms.sourcegitcommit: a9da0abd3e17fbcd6339980d7331d0418cdada53
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/24/2018
ms.locfileid: "34473843"
---
# <a name="sql-server-on-linux"></a>Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server 2017 現在會在 Linux 上執行。 它是相同的 SQL Server 資料庫引擎，有許多類似的功能與服務，不論您的作業系統。

## <a name="install"></a>安裝

若要開始使用，請安裝 SQL Server on Linux 使用其中一種下列快速入門：

- [Red Hat Enterprise Linux 上安裝](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server 上安裝](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安裝](quickstart-install-connect-ubuntu.md)
- [執行 docker](quickstart-install-connect-docker.md)
- [在 Azure 中佈建 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

> [!NOTE]
> Docker 本身會執行多個平台上，這表示您可以在 Linux、 Mac 和 Windows 上執行的 Docker 映像。

## <a name="connect"></a>[連接]

安裝之後，連接到 Linux 機器上的 SQL Server 執行個體。 您可以連接本機或遠端和使用各種工具和驅動程式。 快速入門示範如何使用[sqlcmd](sql-server-linux-setup-tools.md)命令列工具。 其他工具包括下列各項：

| 工具 | 教學課程 |
|-----|-----|
| Visual Studio Code (VS Code) | [使用 VS Code 和 SQL Server on Linux](sql-server-linux-develop-use-vscode.md) |
| SQL Server Management Studio (SSMS) | [在 Windows 上使用 SSMS 連接到 SQL Server on Linux](sql-server-linux-manage-ssms.md) |
| SQL Server Data Tools (SSDT) | [使用 SSDT 搭配 SQL Server on Linux](sql-server-linux-develop-use-ssdt.md) |

## <a name="explore"></a>瀏覽

SQL Server 2017 所有支援的平台，包括 Linux 上有相同的基礎資料庫引擎。 許多現有的特色與功能運作的 Linux 上的方式相同。 文件集的這個區域會顯示其中部分功能以 Linux 的觀點。 它也會呼叫具有獨特需求，在 Linux 上的區域。

如果您已經熟悉 SQL Server，請檢閱[版本資訊](sql-server-linux-release-notes.md)的一般指導方針和此版本的已知的問題。 然後查看[的新功能 SQL Server on Linux](sql-server-linux-whats-new.md)以及[的新功能 SQL Server 2017 整體](../sql-server/what-s-new-in-sql-server-2017.md)。 

> [!TIP]
> 常見問題的解答，請參閱[Linux 常見問題集 > 的 SQL Server](sql-server-linux-faq.md)。

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]