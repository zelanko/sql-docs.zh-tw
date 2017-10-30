---
title: "開發應用程式的 SQL Server on Linux |Microsoft 文件"
description: 
author: sanagama
ms.author: sanagama
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 758cb738-b018-465b-9ab0-59a24b892e66
ms.custom: H1Hack27Feb2017
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: c83b105706916c193cb1a0bbf966ff64fb7bac05
ms.contentlocale: zh-tw
ms.lasthandoff: 10/02/2017

---
# <a name="how-to-get-started-developing-applications-for-sql-server-on-linux"></a>如何開始開發 SQL Server on Linux 應用程式

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

您可以建立連接並使用 SQL Server 2017 從各種不同的程式設計語言，例如 C#、 Java、 Node.js、 PHP、 Python、 Ruby、 和 c + + Linux 上的應用程式。 您也可以使用熱門的 web 架構及物件關聯式對應 (ORM) 架構。

> [!TIP]
> 這些相同的開發選項也可讓您以其他平台上的目標 SQL Server。 應用程式可以在內部部署執行的 SQL Server 為目標或在雲端中，在 Linux、 Windows 或 Docker macOS 上。 或者，您可以針對特定 Azure SQL Database 和 Azure SQL 資料倉儲。

## <a name="try-the-tutorials"></a>請嘗試這些教學課程

若要開始使用並建置應用程式與 SQL Server，最好是自行現在就試試看。

- 瀏覽至[快速入門教學課程](http://aka.ms/sqldev)。
- 選取語言和開發平台。
- 請再試一次的程式碼範例。

> [!TIP]
> 如果您想要開發適用於 docker 的 SQL Server 2017，看看**macOS**教學課程。

## <a name="create-new-applications"></a>建立新的應用程式

如果您要建立新的應用程式，看看一份[連接程式庫](sql-server-linux-develop-connectivity-libraries.md)連接器和適用於各種程式設計語言的常用架構的摘要。

## <a name="use-existing-applications"></a>使用現有的應用程式

如果您有現有的資料庫應用程式，您只可以在 Linux 上的目標 SQL Server 2017，變更其連接字串。 請務必閱讀[已知問題](sql-server-linux-release-notes.md)在 Linux 上的 SQL Server 2017。

## <a name="use-existing-sql-tools-on-windows-with-sql-server-on-linux"></a>使用 SQL Server on Linux 的 Windows 上使用現有的 SQL 工具

此外，目前例如 SSMS、 SSDT 和 PowerShell，在 Windows 執行的工具也會在 Linux 上的 SQL Server 2017 搭配運作。 雖然它們不會執行原生 Linux 上，您仍然可以管理在 Linux 上的遠端 SQL Server 執行個體。 

請參閱下列主題以取得詳細資訊：

- [SQL Server Management Studio (SSMS)](sql-server-linux-develop-use-ssms.md)
- [SQL Server Data Tools (SSDT)](sql-server-linux-develop-use-ssdt.md)
- [SQL PowerShell](sql-server-linux-manage-powershell.md)

> [!Note] 
> 請確定您使用這些工具的最新版本的最佳體驗。

## <a name="use-new-sql-tools-for-linux"></a>使用適用於 Linux 的新 SQL 工具

您可以使用新[mssql 延伸](https://aka.ms/mssql-marketplace)的[Visual Studio Code](https://code.visualstudio.com) Linux、 macOS 及 Windows 上。 如需逐步解說，請參閱下列教學課程：

- [使用 Visual Studio Code](sql-server-linux-develop-use-vscode.md)

您也可以使用都是原生適用於 Linux 的新命令列工具。 這些工具包括下列項目：

- [sqlcmd](../tools/sqlcmd-utility.md)
- [bcp](sql-server-linux-migrate-bcp.md)
- [mssql conf](sql-server-linux-configure-mssql-conf.md)

## <a name="next-steps"></a>後續的步驟

若要開始，請使用下列快速入門教學課程之一 Linux 上安裝 SQL Server:

- [Red Hat Enterprise Linux 上安裝](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server 上安裝](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安裝](quickstart-install-connect-ubuntu.md)
- [執行 docker](quickstart-install-connect-ubuntu.md)

