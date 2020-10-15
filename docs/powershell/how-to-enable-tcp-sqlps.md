---
title: 如何使用 SQLPS 啟用 TCP 通訊協定
description: 了解如何使用 SQLPS 啟用 TCP 通訊協定
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
author: markingmyname
ms.author: maghan
ms.reviewer: matteot
ms.custom: ''
ms.date: 08/06/2020
ms.openlocfilehash: ba4b1362a3f435617f36c75fbcf0e8371169f990
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005166"
---
# <a name="how-to-enable-the-tcp-protocol"></a>如何啟用 TCP 通訊協定

## <a name="how-to-enable-the-tcp-protocol-when-connected-to-the-console-with-sqlps"></a>在使用 SQLPS 連線至主控台時如何啟用 TCP 通訊協定。

[!INCLUDE [sql-server-powershell-version](../includes/sql-server-powershell-version.md)]

1. 開啟命令提示字元，並輸入：

    ```console
    C:\> SQLPS.EXE
    ```

    > [!TIP]
    > 如果找不到 SQLPS，您可能需要開啟新的命令提示字元，或直接登出並重新登入。

2. 在 PowerShell 命令提示字元中，輸入：

    ```powershell
    # Instantiate a ManagedComputer object which exposes primitives to control the
    # installation of SQL Server on this machine.

    $wmi = New-Object 'Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer' localhost

    # Enable the TCP protocol on the default instance. If the instance is named, 
    # replace MSSQLSERVER with the instance name in the following line.

    $tcp = $wmi.ServerInstances['MSSQLSERVER'].ServerProtocols['Tcp']
    $tcp.IsEnabled = $true  
    $tcp.Alter()  

    # You need to restart SQL Server for the change to persist
    # -Force takes care of any dependent services, like SQL Agent.
    # Note: if the instance is named, replace MSSQLSERVER with MSSQL$ followed by
    # the name of the instance (e.g. MSSQL$MYINSTANCE)

    Restart-Service -Name MSSQLSERVER -Force
    ```

## <a name="how-to-enable-the-tcp-protocol-when-connected-to-the-console-not-using-sqlps"></a>在未使用 SQLPS 連線至主控台時如何啟用 TCP 通訊協定。

1. 開啟命令提示字元，並輸入：

    ```console
    C:\> PowerShell.exe
    ```

2. 在 PowerShell 命令提示字元中，輸入：

    ```powershell
    # Get access to SqlWmiManagement DLL on the machine with SQL
    # we are on, which is where SQL Server was installed.
    # Note: this is installed in the GAC by SQL Server Setup.

    [System.Reflection.Assembly]::LoadWithPartialName('Microsoft.SqlServer.SqlWmiManagement')

    # Instantiate a ManagedComputer object which exposes primitives to control the
    # installation of SQL Server on this machine.

    $wmi = New-Object 'Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer' localhost

    # Enable the TCP protocol on the default instance. If the instance is named, 
    # replace MSSQLSERVER with the instance name in the following line.

    $tcp = $wmi.ServerInstances['MSSQLSERVER'].ServerProtocols['Tcp']
    $tcp.IsEnabled = $true  
    $tcp.Alter()  

    # You need to restart SQL Server for the change to persist
    # -Force takes care of any dependent services, like SQL Agent.
    # Note: if the instance is named, replace MSSQLSERVER with MSSQL$ followed by
    # the name of the instance (e.g. MSSQL$MYINSTANCE)

    Restart-Service -Name MSSQLSERVER -Force
    ```

## <a name="next-steps"></a>後續步驟

- [安裝 SQL Server PowerShell 模組](download-sql-server-ps-module.md)
- [SQL Server PowerShell](sql-server-powershell.md)
- [啟用或停用伺服器網路通訊協定](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
- [在 Server Core 安裝上設定 SQL Server](../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md)
