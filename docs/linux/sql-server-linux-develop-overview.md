---
title: 開發 Linux 上 SQL Server 的應用程式
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 11/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 758cb738-b018-465b-9ab0-59a24b892e66
ms.openlocfilehash: 584bf33201cab5d0f57205de0fed181725187d52
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077409"
---
# <a name="how-to-get-started-developing-applications-for-sql-server-on-linux"></a>如何開始開發 Linux 上 SQL Server 的應用程式

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

您可以使用各種程式設計語言 (例如 C#、Java、Node.js、PHP、Python、Ruby 和 C++) 來建立連線至並使用 Linux 上 SQL Server 的應用程式。 您也可以使用熱門的 Web 架構和物件關聯式對應 (ORM) 架構。

> [!VIDEO https://channel9.msdn.com/events/Connect/2017/T153/player]

> [!TIP]
> 這些開發選項也可讓您以其他平台上的 SQL Server 為目標。 應用程式可以將在內部部署或雲端執行的 SQL Server (在 Linux、Windows 或在 MacOS 的 Docker 上) 設為目標。 或者，您也可以將 Azure SQL Database 和 Azure SQL 資料倉儲設為目標。

## <a name="try-the-tutorials"></a>試用教學課程

開始使用及建立應用程式的最佳方式，就是您親自試用 SQL Server。

- 瀏覽至[使用者入門教學課程](https://aka.ms/sqldev)。
- 選取您的語言和開發平台。
- 試用程式碼範例。

> [!TIP]
> 如果您想要針對 Docker 上的 SQL Server 進行開發，請參閱 **macOS** 教學課程。

## <a name="create-new-applications"></a>建立新的應用程式

如果您要建立新的應用程式，請查看[連線程式庫](sql-server-linux-develop-connectivity-libraries.md)的清單，以獲得適用於各種程式設計語言的連接器和熱門架構摘要。

## <a name="use-existing-applications"></a>使用現有的應用程式

如果您擁有現有的資料庫應用程式，您可以直接將其連接字串變更為以 Linux 上的 SQL Server 為目標。 請務必閱讀 Linux 上的 SQL Server 中[已知問題](sql-server-linux-release-notes.md)相關資訊。

## <a name="use-existing-sql-tools-on-windows-with-sql-server-on-linux"></a>使用 Windows 上的現有 SQL 工具，搭配 Linux 上的 SQL Server

目前在 Windows 上執行的工具 (例如 SSMS、SSDT 和 PowerShell) 也適用於 Linux 上的 SQL Server。 雖然它們無法在 Linux 上以原生方式執行，但是您仍然可以在 Linux 上管理遠端 SQL Server 執行個體。 

如需詳細資訊，請參閱下列主題：

- [SQL Server Management Studio (SSMS)](sql-server-linux-manage-ssms.md)
- [SQL Server Data Tools (SSDT)](sql-server-linux-develop-use-ssdt.md)
- [SQL PowerShell](sql-server-linux-manage-powershell.md)

> [!Note]
> 請確定您使用這些工具的最新版本以獲得最佳體驗。

## <a name="use-new-sql-tools-for-linux"></a>使用適用於 Linux 的新 SQL 工具

您可以在 Linux、macOS 和 Windows 上使用適用於 [Visual Studio Code](https://code.visualstudio.com) 的新 [mssql 延伸模組](https://aka.ms/mssql-marketplace)。 如需逐步解說，請參閱下列教學課程：

- [使用 Visual Studio Code](sql-server-linux-develop-use-vscode.md)

您也可以使用適用於 Linux 的原生新命令列工具。 這些工具包括下列項目：

- [sqlcmd](../tools/sqlcmd-utility.md)
- [bcp](sql-server-linux-migrate-bcp.md)
- [mssql-conf](sql-server-linux-configure-mssql-conf.md)

## <a name="next-steps"></a>後續步驟

請使用下列其中一個快速入門來安裝 Linux 上的 SQL Server 以開始使用：

- [在 Red Hat Enterprise Linux 上安裝](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安裝](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安裝](quickstart-install-connect-ubuntu.md)
- [在 Docker 上執行](quickstart-install-connect-ubuntu.md)
