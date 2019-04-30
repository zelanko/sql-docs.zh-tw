---
title: 在 Linux 上的 SQL Server 概觀 |Microsoft Docs
description: 本文說明如何在 Linux 上執行 SQL Server，並提供深入的資訊。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 9dcc6a90-0add-42c2-815b-862e4e2a21ac
ms.openlocfilehash: c24e4fa86c92a183c957c44a33a2d3524cdd1f8c
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "63457371"
---
# <a name="sql-server-on-linux"></a>Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

::: moniker range="= sql-server-2017 || = sqlallproducts-allversions"
SQL Server 從 SQL Server 2017 開始，在 Linux 上執行。 它是相同的 SQL Server 資料庫引擎，與許多類似的功能和服務，不論您的作業系統。
::: moniker-end

::: moniker range=">= sql-server-ver15 || >= sql-server-linux-ver15"
在 Linux 上執行 SQL Server 2019 預覽。 它是相同的 SQL Server 資料庫引擎，與許多類似的功能和服務，不論您的作業系統。 若要深入了解此版本，請參閱[什麼是適用於 Linux 的 SQL Server 2019 preview 的新功能](../sql-server/what-s-new-in-sql-server-ver15.md#sql-server-on-linux)。
::: moniker-end

::: moniker range="= sql-server-2017"
> [!TIP]
> [SQL Server 2019 預覽](sql-server-linux-overview.md?view=sql-server-ver15)已發行 ！ 若要了解新功能適用於 Linux 的最新版本，請參閱[什麼是適用於 Linux 的 SQL Server 2019 preview 的新功能](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux)。
::: moniker-end

::: moniker range="= sql-server-linux-2017"
> [!TIP]
> [SQL Server 2019 預覽](sql-server-linux-overview.md?view=sql-server-linux-ver15)已發行 ！ 若要了解新功能適用於 Linux 的最新版本，請參閱[什麼是適用於 Linux 的 SQL Server 2019 preview 的新功能](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-linux-ver15#sql-server-on-linux)。
::: moniker-end

::: moniker range="= sqlallproducts-allversions"
> [!TIP]
> SQL Server 2019 預覽已發行了 ！ 若要了解新功能適用於 Linux 的最新版本，請參閱[什麼是適用於 Linux 的 SQL Server 2019 preview 的新功能](../sql-server/what-s-new-in-sql-server-ver15.md#sql-server-on-linux)。
::: moniker-end

## <a name="install"></a>安裝

若要開始，請使用下列快速入門的其中一個在 Linux 上安裝 SQL Server:

- [在 Red Hat Enterprise Linux 上安裝](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server 上安裝](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安裝](quickstart-install-connect-ubuntu.md)
- [在 Docker 上執行](quickstart-install-connect-docker.md)
- [在 Azure 中佈建 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

> [!NOTE]
> Docker 本身會在執行多個平台，這表示您可以在 Linux、 Mac 和 Windows 上執行的 Docker 映像。

## <a name="connect"></a>連線

安裝完成後，連線到 Linux 機器上的 SQL Server 執行個體。 您可以連接本機或遠端和使用各種工具和驅動程式。 快速入門示範如何使用[sqlcmd](sql-server-linux-setup-tools.md)命令列工具。 其他工具包括下列各項：

| 工具 | 教學課程 |
|-----|-----|
| Visual Studio Code (VS Code) | [使用 VS Code 和 SQL Server on Linux](sql-server-linux-develop-use-vscode.md) |
| SQL Server Management Studio (SSMS) | [在 Windows 上使用 SSMS 來連線到 Linux 上的 SQL Server](sql-server-linux-manage-ssms.md) |
| SQL Server Data Tools (SSDT) | [使用 SSDT 搭配 SQL Server on Linux](sql-server-linux-develop-use-ssdt.md) |

## <a name="explore"></a>瀏覽

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

SQL Server 2017 已在所有支援的平台，包括 Linux 上的相同的基礎資料庫引擎。 因此，許多現有的特性與功能運作的 Linux 上的方式相同。 文件的這個區域會顯示一些從 Linux 的觀點來看這些功能。 它也會呼叫具有唯一的需求在 Linux 上的區域。

如果您已熟悉 SQL Server，請檢閱[版本資訊](sql-server-linux-release-notes.md)一般指導方針和這個版本的已知的問題。 然後看看[在 Linux 上的 SQL Server 的最新消息](sql-server-linux-whats-new.md)，以及[整體的 SQL Server 2017 最新消息](../sql-server/what-s-new-in-sql-server-2017.md)。

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15"

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 所有支援的平台，包括 Linux 上具有相同的基礎資料庫引擎。 因此，許多現有的特性與功能運作的 Linux 上的方式相同。 文件的這個區域會顯示一些從 Linux 的觀點來看這些功能。 它也會呼叫具有唯一的需求在 Linux 上的區域。

如果您已熟悉 SQL Server on Linux，請檢閱[版本資訊](sql-server-linux-release-notes-2019.md)一般指導方針和這個版本的已知的問題。 然後看看[在 Linux 上的 SQL Server 2019 預覽最新消息](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15)。

::: moniker-end

<!--SQL Server All Versions-->
::: moniker range="=sqlallproducts-allversions"

SQL Server 2017 和[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]所有支援的平台，包括 Linux 上有相同的基礎資料庫引擎。 因此，許多現有的特性與功能運作的 Linux 上的方式相同。 文件的這個區域會顯示一些從 Linux 的觀點來看這些功能。 它也會呼叫具有唯一的需求在 Linux 上的區域。

如果您已經熟悉 SQL Server on Linux，請檢閱版本資訊：

- [SQL Server 2017 版本資訊](sql-server-linux-release-notes.md)
- [SQL Server 2019 preview 版本資訊](sql-server-linux-release-notes-2019.md)

然後，查看最新消息：

- [什麼是 SQL Server 2017 的新功能](sql-server-linux-whats-new.md)
- [新功能在 Linux 上的 SQL Server 2019 preview](../sql-server/what-s-new-in-sql-server-ver15.md#sql-server-on-linux)

::: moniker-end

> [!TIP]
> 如需常見問題的解答，請參閱[Linux 常見問題集 > 的 SQL Server](sql-server-linux-faq.md)。

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
