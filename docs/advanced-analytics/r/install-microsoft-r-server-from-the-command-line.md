---
title: "從命令列安裝 Machine Learning 伺服器 （獨立） 或 Microsoft R Server （獨立） |Microsoft 文件"
ms.custom: 
ms.date: 10/31/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fb4446ba-e9ce-4b93-9854-5e8a58507da0
caps.latest.revision: "4"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 400f743bfbb065a5e271b5ff335d0896bb2ac3ef
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="install-machine-learning-server-standalone-or-microsoft-r-server-standalone-from-the-command-line"></a>從命令列安裝 Machine Learning 伺服器 （獨立） 或 Microsoft R Server （獨立）

本文說明如何使用 SQL Server 命令列引數，若要使用命令列安裝下列的 SQL Server 功能：

+ [機器學習伺服器 （獨立） 在 SQL Server 2017](#bkmk_mls2017) 
+ [在 SQL Server 2016 的 Microsoft R Server （獨立），](#bkmk_mrs2016)

**自動**安裝要求您指定安裝公用程式的位置，並使用引數，表示要安裝的功能。

針對 **無訊息** 安裝，提供相同引數，並新增 **/q** 參數。 會提供任何提示，並不不需要任何互動。 不過，如果省略任何必要的引數時，安裝程式會失敗。

## <a name="prerequisites"></a>必要條件

您應該了解如何執行 SQL Server 的命令列安裝，並熟悉其指令碼的引數。

如需詳細資訊，請參閱[從命令提示字元安裝 SQL Server](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)。

如果您沒有網際網路存取的電腦上安裝 Machine Learning 伺服器或 Microsoft R Server （獨立），您必須事先下載必要的 R （或 Python） 元件，並將它們複製到本機資料夾。 如需下載位置，請參閱[安裝沒有網際網路存取的機器學習元件](installing-ml-components-without-internet-access.md)。


## <a name="bkmk_mls2017"></a>安裝 Microsoft 機器學習服務伺服器 （獨立）

**適用於： SQL Server 2017**

執行下列命令，從提升權限的命令提示字元安裝只有機器學習伺服器 （獨立） 和其必要條件。

+ 功能引數是必要，因為 SQL Server 授權條款。
+ 您可以安裝一個語言，或同時 R 和 Python，但不需要針對每個個別的授權。

此範例顯示用來安裝 r 的引數

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR, SQL_INST_MR  /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

此範例顯示用於安裝 Python 的引數。

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR, SQL_INST_MPY  /IACCEPTPYTHONOPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

+ 若要檢視進度和提示，請移除 _/q_ 引數。
+ 如果您使用引數**功能 = SQL_SHARED_MR**，安裝只機器學習伺服器元件，與 R 都 Python。 此安裝包括所有的先決條件，預設會以無訊息方式安裝。 不過，我們建議您在第一次安裝時新增至少一種語言。
+ 新增**SQL_INST_MR**安裝支援。
+ 新增**SQL_INST_MPY**安裝 Python 的支援。
+ **IACCEPTROPENLICENSETERMS** 表示您已接受授權合約以使用開放原始碼 R 元件。
+ **IACCEPTPYTHONLICENSETERMS**表示您接受授權條款的使用 Python 元件。
+ 需要有**IACCEPTSQLSERVERLICENSETERMS** ，才能執行安裝精靈。


## <a name="bkmk_mrs2016"></a> 安裝 Microsoft R Server (獨立式)

**適用於： SQL Server 2016**

執行下列命令，從提升權限的命令提示字元安裝**只**Microsoft R Server （獨立） 和其必要條件。 

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

> [!TIP]
> 我們建議您不要安裝這裝載 SQL Server R Services 的執行個體在相同電腦上。

## <a name="post-installation-tasks"></a>後續安裝工作

若要設定 Microsoft R Server 的另一個執行個體具有相同參數，您可以重新使用的在安裝期間建立的組態檔。 如需詳細資訊，請參閱[使用組態檔安裝 SQL Server](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md)。

### <a name="review-installed-components"></a>檢閱安裝的元件

安裝程式完成之後，您可以檢閱 SQL Server 安裝程式所建立的組態檔，以及安裝程式動作的摘要。

根據預設，所有 SQL server 安裝程式記錄檔和摘要和相關的功能會建立下列資料夾中：

+ SQL Server 2017:`C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\Log`
+ SQL Server 2016:`C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log`

每個您所安裝的功能會建立個別的子資料夾。

### <a name="customize-the-r-or-python-environment"></a>自訂 R 或 Python 環境

安裝之後，您可以安裝其他的 R 或 Python 封裝。 處理程序不同稍微取決於您使用 SQL Server 2016 或 SQL Server 2017。

在 SQl Server 2017，您可以安裝並使用 T-SQL 來管理的 R 封裝。 如需詳細資訊，請參閱[安裝和管理的 R 封裝](../r/install-additional-r-packages-on-sql-server.md)。

Python 和 SQL Server 2016 中，系統管理員必須安裝可能需要的任何其他程式庫。

> [!IMPORTANT]
> 如果您想要在 SQL Server 上執行 R 程式碼，請確定您將用來進行開發的解決方案，以及您將在其中執行或部署方案的 SQL Server 執行個體在電腦上安裝了相同的封裝。

### <a name="upgrading-r-server-or-sql-server-machine-learning"></a>升級 R Server 或 SQL Server 的機器學習服務

如果您不想要使用 SQL Server，您可以使用個別的 Windows installer 來安裝 Microsoft R Server 或機器學習服務伺服器。 如需下載位置和指示，請參閱以下連結：

+ [安裝機器學習適用於 Windows 的伺服器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [安裝 R Server 9.0.1 適用於 Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) 

機器學習伺服器的個別 windows 安裝程式也可以用於升級的機器學習服務執行個體相關聯的元件。  如需詳細資訊，請參閱下列連結：

+ [使用 SqlBindR 升級 R](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)
