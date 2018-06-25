---
title: 下載並安裝 sqlpackage |Microsoft 文件
description: 下載並安裝適用於 Windows、 macOS 或 Linux sqlpackage
ms.custom: tools|sos
ms.date: 06/18/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: craigg
ms.openlocfilehash: 4e5528ca046de83385171890fbda389928e41cf3
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2018
ms.locfileid: "35703827"
---
# <a name="download-and-install-sqlpackage"></a>下載並安裝 sqlpackage

sqlpackage 會在 Windows、 macOS 和 Linux 上執行。

下載並安裝最新的.NET Framework 版本和 macOS 及 Linux 預覽：

|平台|下載|發行日期|Version|建置|
|:---|:---|:---|:---|:---|
|Windows|[安裝程式](https://go.microsoft.com/fwlink/?linkid=875508)|2018 年 1 月 25 日|17.4.1|14.0.3917.1|
|macOS (預覽)|[.zip](https://go.microsoft.com/fwlink/?linkid=873927)|2018 年 5 月 9 日 |0.0.1|15.0.4057.1|
|Linux (預覽)|[.zip](https://go.microsoft.com/fwlink/?linkid=873926)|2018 年 5 月 9 日 |0.0.1|15.0.4057.1|

## <a name="get-sqlpackage-for-windows"></a>取得 Windows sqlpackage

這個版本的 sqlpackage 包括標準的 Windows 安裝程式經驗，並為.zip: 

**安裝程式**

1. 下載並執行[DacFramework.msi Windows 安裝程式](https://go.microsoft.com/fwlink/?linkid=875508)。
2. 開啟新的命令提示字元視窗，然後執行 sqlpackage.exe
    - sqlpackage 安裝到```C:\Program Files\Microsoft SQL Server\140\DAC\bin```資料夾

## <a name="get-sqlpackage-preview-for-macos"></a>取得 macOS sqlpackage （預覽）

1. 下載[macOS 的 sqlpackage](https://go.microsoft.com/fwlink/?linkid=873927)。
2. 若要將檔案解壓縮，並啟動 sqlpackage，開啟新的終端機視窗並輸入下列命令：

   **.zip 安裝：**
   ```bash 
   mv ~/Downloads/sqlpackage-linux-<version string> ~/sqlpackage 
   echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bash_profile
   source ~/.bash_profile
   sqlpackage 
   ``` 

## <a name="get-sqlpackage-preview-for-linux"></a>取得 sqlpackage （預覽） for Linux

1. 下載[適用於 Linux sqlpackage](https://go.microsoft.com/fwlink/?linkid=873926)使用其中一種安裝程式或.tar.gz 封存：
2. 若要將檔案解壓縮，並啟動 sqlpackage，開啟新的終端機視窗並輸入下列命令：

   **.zip 安裝：**
   ```bash 
   cd ~ 
   mkdir sqlpackage
   unzip ~/Downloads/sqlpackage-linux-<version string>.zip ~/sqlpackage 
   echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bashrc
   source ~/.bashrc 
   sqlpackage 
   ``` 

   > [!NOTE]
   > 在 Debian、 Redhat 和 Ubuntu，您可能遺失相依性。 若要安裝這些相依性，根據您的 Linux 版本中使用下列命令：
   

   **Debian:** 
   ```bash
   sudo apt-get install libuwind8
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


## <a name="uninstall-sqlpackage-preview"></a>解除安裝 sqlpackage （預覽）

如果您安裝 sqlpackage 使用 Windows installer，然後解除安裝移除所有 Windows 應用程式的方式相同。

如果您安裝 sqlpackage.zip 或其他封存，只要刪除檔案。

## <a name="supported-operating-systems"></a>支援的作業系統

sqlpackage Windows、 macOS 和 Linux 上執行，並支援下列平台：

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
- macOS 10.13 高利也
- macOS 10.12 利也

### <a name="linux-x64"></a>Linux (x64)
- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="next-steps"></a>Next Steps

- 深入了解[sqlpackage](sqlpackage.md)

[Microsoft 隱私權聲明](https://go.microsoft.com/fwlink/?LinkId=521839)
