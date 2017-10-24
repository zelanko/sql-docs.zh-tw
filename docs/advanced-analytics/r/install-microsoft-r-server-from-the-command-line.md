---
title: "從命令列安裝 Microsoft R Server | Microsoft Docs"
ms.custom: 
ms.date: 04/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fb4446ba-e9ce-4b93-9854-5e8a58507da0
caps.latest.revision: 4
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: b9f6ceba4d3609a7e7ff816d31446a77c4fea64c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="install-microsoft-r-server-from-the-command-line"></a>從命令列安裝 Microsoft R Server
    
本主題描述如何使用 SQL Server 命令列引數來安裝 Microsoft R Server 在 SQL Server 2016 中，或安裝在 SQL Server 2017 機器學習伺服器 （獨立）。 

> [!NOTE]
您也可以使用個別的 Windows installer 安裝 Microsoft R Server。 如需詳細資訊，請參閱[安裝 R 9.0.1 適用於 Windows Server](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)。 

## <a name="prerequisites"></a>必要條件

此安裝方法需要您知道如何執行 SQL Server 的命令列安裝，並熟悉其指令碼的引數。

- **自動** 安裝需要您指定安裝程式公用程式的位置，並使用引數表示要安裝的功能。 
- 針對 **無訊息** 安裝，提供相同引數，並新增 **/q** 參數。 將不會提供任何提示，也不需要任何互動。 不過，如果省略任何必要引數，則安裝程式會失敗。

如需詳細資訊，請參閱 [從命令提示字元安裝 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)。

## <a name="sql-server-2017-microsoft-machine-learning-server-standalone"></a>SQL Server 2017: Microsoft 機器學習服務伺服器 （獨立）

執行下列命令，從提升權限的命令提示字元安裝只有 Microsoft 機器學習伺服器 （獨立） 和其必要條件。  此範例顯示用來安裝 r 的引數

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR, SQL_INST_MR  /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS 
```

若要檢視進度和提示，請移除 _/q_ 引數。

- **功能 = SQL_SHARED_MR**取得機器學習伺服器元件。 這包括任何預設會以無訊息模式安裝的必要條件。
- **SQL_INST_MR**無須 installl 的 R 語言的支援。
- **SQL_INST_MPY**才能安裝 Python 的支援。
- **IACCEPTROPENLICENSETERMS** 表示您已接受授權合約以使用開放原始碼 R 元件。
- **IACCEPTPYTHONLICENSETERMS**表示您接受授權條款的使用 Python 元件。
- 需要有**IACCEPTSQLSERVERLICENSETERMS** ，才能執行安裝精靈。

**注意**

1. 功能引數是必要，因為 SQL Server 授權條款。
2. 指定至少一種語言，以及授權的協議旗標。
3. 您可以安裝一個語言，或同時 R 和 Python，但不需要針對每個個別的授權。

## <a name="sql-server-2016-microsoft-r-server-standalone"></a>SQL Server 2016: Microsoft R Server （獨立）

從提升權限的命令提示字元執行下列命令，僅安裝 Microsoft R Server (獨立) 和其必要條件。  此範例會示範搭配 SQL Server 2016 安裝程式的引數。

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

## <a name="offline-installation"></a>離線安裝

如果您沒有網際網路存取的電腦上安裝 Machine Learning 伺服器或 Microsoft R Server （獨立），您必須事先下載必要的 R 元件，並將它們複製到本機資料夾。 如需下載位置，請參閱 [安裝沒有網際網路存取的 R 元件](../r/installing-ml-components-without-internet-access.md)。

## <a name="what-is-installed"></a>安裝的內容

安裝程式完成之後，您可以檢閱 SQL Server 安裝程式所建立的組態檔，以及安裝程式動作的摘要。

根據預設，所有 SQL server 安裝程式記錄檔和摘要和相關的功能會建立下列資料夾中：

- SQL Server 2016:`C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log`
- SQL Server 2017:`C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\Log`

會為安裝的每個功能建立個別的子資料夾。

若要設定 Microsoft R Server 的另一個執行個體具有相同參數，您可以重新使用的在安裝期間建立的組態檔。 如需詳細資訊，請參閱[使用組態檔安裝 SQL Server](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)


## <a name="customize-your-r-environment"></a>自訂您的 R 環境

安裝之後，您可以安裝其他 R 套件。 如需詳細資訊，請參閱 [安裝和管理 R 套件](../r/install-additional-r-packages-on-sql-server.md)。

> [!IMPORTANT]
> 如果您想要在 SQL Server 上執行 R 程式碼，請確定您將用來進行開發的解決方案，以及您將在其中執行或部署方案的 SQL Server 執行個體在電腦上安裝了相同的封裝。

安裝 R （資料庫） 的機器學習服務之後，您可以使用個別的 Windows 安裝程式來升級指定的 SQL Server 執行個體相關聯的 R 版本。 如需詳細資訊，請參閱[來升級 R 使用 SqlBindR](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。



