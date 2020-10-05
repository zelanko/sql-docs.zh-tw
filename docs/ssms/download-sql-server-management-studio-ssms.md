---
title: 下載 SQL Server Management Studio (SSMS)
description: 下載最新版的 SQL Server Management Studio (SSMS)。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
keywords:
- 安裝 ssms, 下載 ssms, 最新的 ssms
- SQL Server Management Studio
- ssms.exe
- sql man studio
- sql management studio
- sql management studio install
- download sql management studio
- ms sql management studio
- install sql management studio
- ssms download
- sql server ssms
- ssms express
ms.assetid: adafeeef-4255-4924-8042-02f503d599ca
author: dzsquared
ms.author: drskwier
manager: viharp
ms.reviewer: maghan
ms.custom: seo-lt-2019
ms.date: 09/28/2020
ms.openlocfilehash: 23137d46453189bb5a04c2860ab79c0c66e8d78f
ms.sourcegitcommit: 2600a414c321cfd6dc6daf5b9bcbc9a99c049dc4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/30/2020
ms.locfileid: "91603468"
---
# <a name="download-sql-server-management-studio-ssms"></a>下載 SQL Server Management Studio (SSMS)

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

SQL Server Management Studio (SSMS) 是整合式環境，可用於管理任何 SQL 基礎結構，從 SQL Sever 到 Azure SQL Database 皆適用。 SSMS 提供工具來設定、監視以及管理 SQL Server 執行個體和資料庫。 使用 SSMS，即可部署、監視和升級應用程式所使用的資料層元件，以及建置查詢和指令碼。

使用 SSMS，即可查詢、設計與管理資料庫和資料倉儲，而不論它們位在何處：本機電腦上或雲端中。

SSMS 是免費的！

## <a name="download-ssms"></a>下載 SSMS

:::image type="icon" source="media/download-icon.png" border="false"::: **[下載 SQL Server Management Studio (SSMS)](https://aka.ms/ssmsfullsetup)**

SSMS 18.6 是 SSMS 最新的正式發行 (GA) 版本。 若先前已安裝 SSMS 18 的 GA 版本，則安裝 SSMS 18.6 會將其升級至 18.6。

### <a name="version-information"></a>版本資訊

- 版本號碼：18.6
- 組建編號：15.0.18338.0
- 發行日期：2020 年 7 月 22 日

若您有意見或建議，或是要回報問題，則連絡 SSMS 小組的最佳方式是透過 [SQL Server 使用者意見反應](https://aka.ms/sqlfeedback)。

SSMS 18.x 安裝不會升級或取代 SSMS 17.x 版或更早版本。 SSMS 18.x 會與舊版本並行安裝，以便於使用者能夠同時使用這兩種版本。 不過，如果您已安裝 SSMS 18.x「預覽」版本，則必須在安裝 SSMS 18.6 前先將其解除安裝。 可以前往 [說明] > [關於]  視窗，以查看您是否有預覽版本。

如果電腦中包含並存安裝的 SSMS，請確認已針對您的特定需求啟動正確的版本。 最新版本會標記為 **Microsoft SQL Server Management Studio 18**

> [!Note]
> 如果您在非英文語言版本存取此頁面，且想要查看最新內容，請參閱[本頁面的英文 (美國) 版](https://aka.ms/downloadssmsusenglish)。 您可以選取[可用的語言](#available-languages)，從英文 (美國) 版網站下載不同語言版本。

## <a name="available-languages"></a>可用的語言

此版 SSMS 提供下列語言版本：

SQL Server Management Studio 18.6：  
[簡體中文](https://go.microsoft.com/fwlink/?linkid=2135491&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2135491&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2135491&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2135491&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2135491&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2135491&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2135491&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2135491&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2135491&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2135491&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2135491&clcid=0x40a)

> [!NOTE]
> SQL Server PowerShell 模組為透過 PowerShell 資源庫個別安裝的模組。 如需詳細資訊，請參閱[下載 SQL Server PowerShell 模組](download-sql-server-ps-module.md)。

## <a name="whats-new"></a>新功能

如需此版本中最新功能的詳細資訊，請參閱 [SSMS 版本資訊](release-notes-ssms.md)。

此版本有一些[已知問題](release-notes-ssms.md#known-issues-186)。

## <a name="previous-versions"></a>舊版

本文僅適用於最新版本的 SSMS。 若要下載舊版的 SSMS，請前往[舊版 SSMS](../ssms/release-notes-ssms.md#previous-ssms-releases)。

[!INCLUDE[ssms-connect-azure-ad](../includes/ssms-connect-azure-ad.md)]

## <a name="unattended-install"></a>自動安裝

您也可以使用命令提示字元指令安裝 SSMS。

苦要在不提供 GUI 提示的背景中安裝 SSMS，請執行下列步驟。

1. 啟動權限較高的命令提示字元。

2. 在下列命令提示字元中鍵入命令。

    ```console
    start "" /w <path where SSMS-ENU.exe file is located> /Quiet SSMSInstallRoot=<path where you want to install SSMS>
    ```

    範例：

    ```console
    start "" /w %systemdrive%\SSMSfrom\SSMS-Setup-ENU.exe /Quiet SSMSInstallRoot=%systemdrive%\SSMSto
    ```

    您也可以傳遞 /Passive  (而不是 /Quiet  )，以查看安裝程式 UI。

3. 若一切順利，就會像範例般顯示安裝在 %systemdrive%\SSMSto\Common7\IDE\Ssms.exe 的 SSMS。 若發生錯誤，將能查看傳回的錯誤碼，以及 %TEMP%\SSMSSetup 中的記錄檔。

## <a name="uninstall"></a>解除安裝

在您將 SSMS 解除安裝之後，某些共用元件仍會維持安裝。

維持安裝的共用元件為：

- Microsoft .NET Framework 4.7.2
- Microsoft OLE DB Driver for SQL Server
- Microsoft ODBC Driver 17 for SQL Server
- Microsoft Visual C++ 2013 可轉散發套件 (x86)
- Microsoft Visual C++ 2017 可轉散發套件 (x86)
- Microsoft Visual C++ 2017 可轉散發套件 (x64)
- Microsoft Visual Studio Tools for Applications 2017

這些元件可以與其他產品共用，因此不會解除安裝。 若解除安裝，可能會導致其他產品無法使用。

## <a name="supported-sql-offerings"></a>支援的 SQL 供應項目

- 此版本的 SSMS 適用於所有[支援的 SQL Server 2008 - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044)，並提供最高層級的支援以使用 Azure SQL Database 和 Azure SQL 資料倉儲中最新雲端功能。
- 此外，SSMS 18.x 可以與 SSMS 17.x、SSMS 16.x 或 SQL Server 2014 SSMS 及更早的版本並存安裝。
- SQL Server Integration Services (SSIS) - SSMS 17.x 或更新版本不支援連線至舊版 SQL Server Integration Services 服務。 若要連線至舊版 Integration Services 的舊版本，請使用與 SQL Server 版本一致的 SSMS 版本。 例如，使用 SSMS 16.x 連線至舊版 SQL Server 2016 Integration Services 服務。 SSMS 17.x 和 SSMS 16.x 可以並存安裝在相同電腦上。 自 SQL Server 2012 發行之後，建議使用 SSIS Catalog 資料庫 SSISDB 來儲存、管理、執行和監視 Integration Services 套件。 如需詳細資訊，請參閱 [SSIS 目錄](../integration-services/catalog/ssis-catalog.md)。

## <a name="ssms-system-requirements"></a>SSMS 系統需求

搭配最新推出的服務套件使用時，這一版 SSMS 支援下列 64 位元平台：

支援的作業系統：

- Windows 10 (64 位元) 版本 1607 (10.0.14393) 或更新版本
- Windows 8.1 (64 位元)
- Windows Server 2019 (64 位元)
- Windows Server 2016 (64 位元)
- Windows Server 2012 R2 (64 位元)
- Windows Server 2012 (64 位元)
- Windows Server 2008 R2 (64 位元)

支援的硬體：

- 1.8 GHz 或更快的 x86 (Intel、AMD) 處理器。 建議雙核心或更佳的處理器
- 2 GB 的 RAM，建議 4 GB 的 RAM (如果在虛擬機器上執行，至少 2.5 GB)
- 硬碟空間：最少 2 GB 至 10 GB 的可用空間

> [!NOTE]
> SSMS 僅能在 Windows 上執行。 若您需要能在 Windows 以外作業系統上執行的工具，我們建議使用 Azure Data Studio。 Azure Data Studio 是一個跨平台工具，可在 macOS、Linux 與 Windows 上執行。 如需詳細資料，請參閱 [Azure Data Studio](../azure-data-studio/what-is.md)。

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

## <a name="next-steps"></a>後續步驟

- [教學課程：SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [SQL Server Management Studio 文件](sql-server-management-studio-ssms.md)
- [最新的更新](../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)
- [Azure Data Studio](../azure-data-studio/what-is.md)
- [下載 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)
- [Azure 資料架構指南](https://docs.microsoft.com/azure/architecture/data-guide/)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
