---
title: 下載並安裝 sqlpackage | Microsoft Docs
description: 下載並安裝適用於 Windows、macOS 或 Linux 的 sqlpackage
ms.custom: tools|sos
ms.date: 06/20/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
ms.openlocfilehash: 01654df047d2dc78014c6e8c41edbb370d15da60
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874396"
---
# <a name="download-and-install-sqlpackage"></a>下載並安裝 sqlpackage

sqlpackage 在 Windows、macOS 和 Linux 上執行。

下載並安裝最新的 .NET Framework 版本以及 macOS 和 Linux 預覽：

|平台|下載|發行日期|Version|建置
|:---|:---|:---|:---|:---|
|Windows|[MSI 安裝程式](https://go.microsoft.com/fwlink/?linkid=2102893)|2019年9月6日|18。3|15.0.4532.1|
|macOS .NET Core (預覽)|[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2102894)|2019年9月6日| 18。3|15.0.4532.1|
|Linux .NET Core (預覽)|[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2102978)|2019年9月6日| 18。3|15.0.4532.1|
|Windows .NET Core （預覽）|[壓縮檔](https://go.microsoft.com/fwlink/?linkid=2102979)|2019年9月6日| 18。3|15.0.4532.1|

如需最新版本的詳細資訊，請參閱[版本資訊](release-notes-sqlpackage.md)。

[!INCLUDE[Freshness](../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="get-sqlpackage-for-windows"></a>取得適用於 Windows 的 sqlpackage

此版本的 sqlpackage 包含標準的 Windows 安裝程式體驗，以及 .zip： 

1. 下載並執行[適用於Windows 的 DacFramework.msi 安裝程式](https://go.microsoft.com/fwlink/?linkid=2102893)。
2. 開啟新的 [命令提示字元] 視窗，然後執行 sqlpackage.exe
    - sqlpackage 會安裝到 ```C:\Program Files\Microsoft SQL Server\150\DAC\bin``` 資料夾中
    - 在 x64 電腦上安裝 x86 版本，sqlpackage 會安裝在 ```C:\Program Files (x86)\Microsoft SQL Server\150\DAC\bin``` 資料夾中

## <a name="get-sqlpackage-net-core-preview-for-windows"></a>取得適用于 Windows 的 sqlpackage .NET Core （預覽）

1. 下載 [sqlpackage for Windows](https://go.microsoft.com/fwlink/?linkid=2102979)。
2. 以滑鼠右鍵按一下 Windows Explorer 中的檔案，然後選取 [解壓縮全部]，然後選取目標目錄，來解壓縮檔案。
3. 開啟新的終端機視窗，可以 cd 到 exracted sqlpackage 的位置：

   **.zip 安裝：**

   ```bash
   sqlpackage
   ```

## <a name="get-sqlpackage-net-core-preview-for-macos"></a>取得適用于 macOS 的 sqlpackage .NET Core （預覽）

1. 下載[適用於 macOS 的 sqlpackage](https://go.microsoft.com/fwlink/?linkid=2102894)。
2. 若要將檔案解壓縮並啟動 sqlpackage，請開啟新的終端機視窗並輸入下列命令：

   **.zip 安裝：**

   ```bash
   mkdir sqlpackage
   unzip ~/Downloads/sqlpackage-osx-<version string>.zip ~/sqlpackage 
   echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bash_profile
   source ~/.bash_profile
   sqlpackage
   ```

## <a name="get-sqlpackage-net-core-preview-for-linux"></a>取得適用于 Linux 的 sqlpackage .NET Core （預覽）

1. 使用其中一種安裝程式或 tar.gz 封存下載[適用於 Linux 的 sqlpackage](https://go.microsoft.com/fwlink/?linkid=2102978)：
2. 若要將檔案解壓縮並啟動 sqlpackage，請開啟新的終端機視窗並輸入下列命令：

   **.zip 安裝：**

   ```bash
   cd ~
   mkdir sqlpackage
   unzip ~/Downloads/sqlpackage-linux-<version string>.zip -d ~/sqlpackage 
   echo "export PATH=\"\$PATH:$HOME/sqlpackage\"" >> ~/.bashrc
   chmod a+x ~/sqlpackage/sqlpackage
   source ~/.bashrc
   sqlpackage
   ```

   > [!NOTE]
   > 在 Debian、Redhat 和 Ubuntu 上，您可能遺失相依性。 使用下列命令，根據您的 Linux 版本安裝這些相依性：

   **Debian：**

   ```bash
   sudo apt-get install libunwind8
   ```

   **Redhat:**

   ```bash
   yum install libunwind
   yum install libicu
   ```

   **Ubuntu:**

   ```bash
   sudo apt-get install libunwind8

   # install the libicu library based on the Ubuntu version
   sudo apt-get install libicu52      # for 14.x
   sudo apt-get install libicu55      # for 16.x
   sudo apt-get install libicu57      # for 17.x
   sudo apt-get install libicu60      # for 18.x
   ```

## <a name="uninstall-sqlpackage-preview"></a>解除安裝 sqlpackage (預覽)

如果您使用 Windows 安裝程式安裝 sqlpackage，請使用與刪除任何 Windows 應用程式相同的方式解除安裝。

如果您使用 .zip 或其他封存安裝 sqlpackage，則只需刪除這些檔案即可。

## <a name="supported-operating-systems"></a>支援的作業系統

sqlpackage 在 Windows、macOS 和 Linux 上執行，並支援下列平台：

### <a name="windows"></a>Windows

- Windows 10
- Windows 8.1
- Windows 8
- Windows 7 SP1
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2

### <a name="macos"></a>macOS

- macOS 10.13 High Sierra
- macOS 10.12 Sierra

### <a name="linux-x64"></a>Linux (x64)

- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="next-steps"></a>Next Steps

- 深入了解 [sqlpackage](sqlpackage.md)

[Microsoft 隱私權聲明](https://go.microsoft.com/fwlink/?LinkId=521839)
