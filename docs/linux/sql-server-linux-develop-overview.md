---
title: 針對 Linux 上的 SQL Server 開發應用程式 |Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/17/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.custom: sql-linux
ms.suite: sql
ms.technology: linux
ms.assetid: 758cb738-b018-465b-9ab0-59a24b892e66
ms.openlocfilehash: 317c2ea2064f7ffc286671a8fff7eef2f8149ee7
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39084915"
---
# <a name="how-to-get-started-developing-applications-for-sql-server-on-linux"></a>如何開始開發應用程式在 Linux 上的 SQL server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

您可以建立應用程式連接到並使用從各種程式設計語言，例如 C#、 Java、 Node.js、 PHP、 Python、 Ruby 和 c + + 的 Linux 上的 SQL Server 2017。 您也可以使用熱門的 web 架構和物件關聯式對應 (ORM) 架構。

> [!VIDEO https://channel9.msdn.com/events/Connect/2017/T153/player]

> [!TIP]
> 這些相同的開發選項也可讓您以其他平台上的目標 SQL Server。 目標應用程式可以執行內部部署的 SQL Server 或在雲端、 Linux、 Windows 或 Docker 上在 macOS 上。 或者，您可以為 Azure SQL Database 和 Azure SQL 資料倉儲目標。

## <a name="try-the-tutorials"></a>嘗試教學課程

開始使用，並使用 SQL Server 建置應用程式的最佳方式是親自試用。

- 瀏覽至[快速入門教學課程](http://aka.ms/sqldev)。
- 選取您的語言和開發平台。
- 嘗試的程式碼範例。

> [!TIP]
> 如果您想要在 Docker 上的 SQL Server 2017 的開發，看看**macOS**教學課程。

## <a name="create-new-applications"></a>建立新的應用程式

如果您要建立新的應用程式，看看一份[連線程式庫](sql-server-linux-develop-connectivity-libraries.md)連接器和熱門的架構，適用於各種程式設計語言的摘要。

## <a name="use-existing-applications"></a>使用現有的應用程式

如果您有現有的資料庫應用程式時，您只可以在目標 SQL Server 2017 Linux 上，變更其連接字串。 請務必閱讀[已知問題](sql-server-linux-release-notes.md)在 Linux 上的 SQL Server 2017。

## <a name="use-existing-sql-tools-on-windows-with-sql-server-on-linux"></a>Windows 與 Linux 上的 SQL Server 上使用現有的 SQL 工具

目前 SSMS、 SSDT 和 PowerShell，例如 Windows 執行的工具也適用於 Linux 上的 SQL Server 2017。 雖然它們未執行原生 Linux 上，您還是可以管理在 Linux 上的遠端 SQL Server 執行個體。 

請參閱下列主題中的詳細資訊：

- [SQL Server Management Studio (SSMS)](sql-server-linux-manage-ssms.md)
- [SQL Server Data Tools (SSDT)](sql-server-linux-develop-use-ssdt.md)
- [SQL PowerShell](sql-server-linux-manage-powershell.md)

> [!Note]
> 請確定您使用這些工具的最新版本以獲得最佳體驗。

## <a name="use-new-sql-tools-for-linux"></a>使用適用於 Linux 的新 SQL 工具

您可以使用新[mssql 擴充功能](https://aka.ms/mssql-marketplace)for [Visual Studio Code](https://code.visualstudio.com) Linux、 macOS 和 Windows 上。 如需逐步解說，請參閱下列教學課程：

- [使用 Visual Studio Code](sql-server-linux-develop-use-vscode.md)

您也可以使用新的原生適用於 Linux 的命令列工具。 這些工具包括下列項目：

- [sqlcmd](../tools/sqlcmd-utility.md)
- [bcp](sql-server-linux-migrate-bcp.md)
- [mssql-conf](sql-server-linux-configure-mssql-conf.md)

## <a name="next-steps"></a>後續步驟

若要開始，請使用下列快速入門的其中一個在 Linux 上安裝 SQL Server:

- [在 Red Hat Enterprise Linux 上安裝](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server 上安裝](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安裝](quickstart-install-connect-ubuntu.md)
- [在 Docker 上執行](quickstart-install-connect-ubuntu.md)
