---
title: "SQL Server on Linux 的概觀 |Microsoft 文件"
description: "本主題描述 SQL Server 如何在 Linux 上執行，並提供如何了解詳細資訊。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 08/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9dcc6a90-0add-42c2-815b-862e4e2a21ac
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 1192afb7032f34f0af98c3c1051808e89dc22b63
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="sql-server-on-linux"></a>Linux 上的 SQL Server

現在 Linux 上執行 SQL Server ！ 這個最新版本中，SQL Server 2017 RC2，在執行 Linux 上，而且會在許多方面直接 SQL Server。 它是相同的 SQL Server 資料庫引擎，有許多類似的功能與服務，不論您的作業系統。

## <a name="install"></a>Install

若要開始，請使用下列快速入門教學課程之一 Linux 上安裝 SQL Server:

- [Red Hat Enterprise Linux 上安裝](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server 上安裝](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安裝](quickstart-install-connect-ubuntu.md)
- [執行 docker](quickstart-install-connect-docker.md)

> [!NOTE]
> Docker 本身會執行多個平台上，這表示您可以在 Linux、 Mac 和 Windows 上執行的 Docker 映像。

## <a name="connect"></a>Connect

安裝之後，連接到 Linux 機器上的 SQL Server 執行個體。 您可以連接本機或遠端和使用各種工具和驅動程式。 快速入門教學課程會示範如何使用[sqlcmd](sql-server-linux-setup-tools.md)命令列工具。 其他工具包括下列各項：

| 工具 | 教學課程 |
|-----|-----|
| Visual Studio 程式碼 (VS Code) | [使用 VS 程式碼和 SQL Server on Linux](sql-server-linux-develop-use-vscode.md) |
| SQL Server Management Studio (SSMS) | [在 Windows 上使用 SSMS 連接到 SQL Server on Linux](sql-server-linux-develop-use-ssms.md) |
| SQL Server Data Tools (SSDT) | [使用 SSDT 搭配 SQL Server on Linux](sql-server-linux-develop-use-ssdt.md) |

## <a name="explore"></a>瀏覽

SQL Server 2017 所有支援的平台，包括 Linux 上有相同的基礎資料庫引擎。 許多現有的特色與功能運作的 Linux 上的方式相同。 文件集的這個區域會顯示其中部分功能以 Linux 的觀點。 它也會呼叫具有獨特需求，在 Linux 上的區域。

如果您已經熟悉 SQL Server，請檢閱[版本資訊](sql-server-linux-release-notes.md)的一般指導方針和此版本的已知的問題。 然後查看[的新功能 SQL Server on Linux](sql-server-linux-whats-new.md)以及[的新功能 SQL Server 2017 整體](../sql-server/what-s-new-in-sql-server-2017.md)。

##  <a name="infotipmediageneralinfotippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](./media/general/info_tip.png) 與 SQL Server 工程團隊交流

- [DBA 堆疊 Exchange](https://dba.stackexchange.com/questions/tagged/sql-server)： 提問資料庫管理
- [堆疊溢位](http://stackoverflow.com/questions/tagged/sql-server)： 開發提問
- [MSDN 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)： 詢問技術問題
- [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback)： 報告錯誤和要求的功能
- [Reddit](https://www.reddit.com/r/SQLServer/)： 討論 SQL Server

