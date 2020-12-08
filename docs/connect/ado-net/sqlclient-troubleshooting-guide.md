---
title: SqlClient 疑難排解指南
description: 為常見問題提供解決方法的頁面。
ms.date: 11/27/2020
dev_langs:
- csharp
- vb
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-jizho2
ms.openlocfilehash: 6cad6278eb6ac7b170ee108c1a3510db956ecb22
ms.sourcegitcommit: 0c0e4ab90655dde3e34ebc08487493e621f25dda
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2020
ms.locfileid: "96468081"
---
# <a name="sqlclient-troubleshooting-guide"></a>SqlClient 疑難排解指南

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

## <a name="exceptions-when-connecting-to-sql-server"></a>連線到 SQL Server 時發生例外狀況

有許多原因會導致無法建立連線。 以下是一些疑難排解提示，可作為分析及解決許多問題的指南。

### <a name="unable-to-load-native-sni-server-name-indication-library"></a>無法載入原生 SNI (伺服器名稱指示) 程式庫

#### <a name="issues-in-net-framework-applications"></a>.NET Framework 應用程式中的問題

觀察到的 StackTrace：

```log
TypeInitializationException: The type initializer for 'Microsoft.Data.SqlClient.SNILoadHandle' threw an exception.
DllNotFoundException: Unable to load DLL 'Microsoft.Data.SqlClient.SNI.x64.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)
```

```log
TypeInitializationException: The type initializer for 'Microsoft.Data.SqlClient.SNILoadHandle' threw an exception.
DllNotFoundException: Unable to load DLL 'Microsoft.Data.SqlClient.SNI.x86.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)
```

SNI 是 SqlClient 在 Windows 上執行時，於各種網路作業上皆須仰賴的原生 C++ 程式庫。 在使用 MSBuild 專案 SDK 建置的 .NET Framework 應用程式中，原生 DLL 不是以還原命令來管理。 因此會將 ".targets" 檔案包含在 "Microsoft.Data.SqlClient.SNI" NuGet 套件中，以定義必要的「複製」作業。

對 "Microsoft.Data.SqlClient" 程式庫建立直接相依性時，會自動參考所包含的 ".targets" 檔案。 在做出可轉移 (間接) 參考的案例中，應該要手動參考此 ".targets" 檔案，以確保「複製」作業可以在必要時執行。

**建議的解決方案：** 確定已在應用程式的 ".csproj" 檔案中參考 ".targets" 檔案，以確保會執行「複製」作業。

這些目標僅會涵蓋 Microsoft 較知名且廣為使用的目標。 如果外部工具或應用程式會定義自訂目標以複製二進位檔，工具維護人員必須定義新的目標，以確保原生 SNI DLL 會與 Microsoft.Data.SqlClient.dll 二進位檔一起複製，而且在執行用戶端應用程式時可供使用。

#### <a name="issues-in-net-core-applications"></a>.NET Core 應用程式中的問題

觀察到的 StackTrace：

```log
System.TypeInitializationException: The type initializer for 'Microsoft.Data.SqlClient.TdsParser' threw an exception.
---> System.TypeInitializationException: The type initializer for 'Microsoft.Data.SqlClient.SNILoadHandle' threw an exception.
---> System.DllNotFoundException: Unable to load shared library 'Microsoft.Data.SqlClient.SNI.dll' or one of its dependencies.
```

> [!NOTE]
> 此錯誤只會在 Windows 應用程式上發生。 如果其在 Unix 環境中發生，您必須確保應用程式已建置為能夠適當地以 Unix 執行階段為目標，而不是針對 Windows。

SNI 是 SqlClient 在 Windows 上執行時，於各種網路作業上皆須仰賴的原生 C++ 程式庫。 Microsoft.Data.SqlClient 不會管理此程式庫在 .NET Core 中的載入/卸載。

**建議的解決方案：** 確定已在於 .NET Core 處理序中載入原生執行階段程式庫的檔案系統上授與「執行」權限。 如果那無法解決問題，您可以在 [dotnet/runtime](https://github.com/dotnet/runtime) \(英文\) 存放庫中提出問題以取得進一步支援。

#### <a name="native-sni-pdb-not-found-errors"></a>原生 SNI (找不到 pdb) 錯誤

觀察到的 StackTrace：

```log
An assembly specified in the application dependencies manifest (sql2csv.deps.json) was not found:
  package: 'Microsoft.Data.SqlClient.SNI.runtime', version: '2.0.0'
  path: 'runtimes/win-x64/native/Microsoft.Data.SqlClient.SNI.pdb'
```

**建議的解決方案：** 確定用戶端應用程式至少是參考 [v2.1.0](https://www.nuget.org/packages/Microsoft.Data.SqlClient/2.1.0) \(英文\) 版的 Microsoft.Data.SqlClient 套件。 使用 EF Core 時，請直接新增此 Microsoft.Data.SqlClient 套件版本的參考以覆寫相依性。

### <a name="hostname-resolution-errors"></a>主機名稱解析錯誤

觀察到的 StackTrace：

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible.
Verify that the instance name is correct and that SQL Server is configured to allow remote connections.
(provider: TCP Provider, error: 0 - No such host is known.)
```

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible.
Verify that the instance name is correct and that SQL Server is configured to allow remote connections.
(provider: TCP Provider, error: 35 - An internal exception was caught)
```

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible.
Verify that the instance name is correct and that SQL Server is configured to allow remote connections.
(provider: TCP Provider, error: 35 - An internal exception was caught)
 ---> System.Net.Internals.SocketExceptionFactory+ExtendedSocketException (00000005, 0xFFFDFFFF): Name does not resolve
```

#### <a name="possible-reasons"></a>可能的原因

- 未在 SQL Server 上啟用 TCP/具名管道通訊協定

  **建議的解決方案：** 從 SQL Server 組態管理員主控台啟用 SQL Server 執行個體上的 TCP/具名管道通訊協定。

- 未知的主機名稱

  **建議的解決方案：** 確定主機名稱能從起始連線的用戶端解析到伺服器的 IP 位址。


### <a name="login-phase-errors"></a>登入階段錯誤

觀察到的 StackTrace：

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): A connection was successfully established with the server, but then an error occurred during the pre-login handshake.
(provider: SSL Provider, error: 31 - Encryption(ssl/tls) handshake failed)
System.IO.EndOfStreamException: End of stream reached
```

```log
A connection was successfully established with the server, but then an error occurred during the login process.
(provider: SSL Provider, error: 0 - The target principal name is incorrect.)
```

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): Connection Timeout Expired. The timeout period elapsed during the post-login phase. The connection could have timed out while waiting for server to complete the login process and respond; Or it could have timed out while attempting to create multiple active connections.
The duration spent while attempting to connect to this server was - [Pre-Login] initialization=837; handshake=394; [Login] initialization=3; authentication=15; [Post-Login] complete=1027;
---> System.ComponentModel.Win32Exception (258): Unknown error 258
at Microsoft.Data.SqlClient.SqlInternalConnection.OnError(SqlException exception, Boolean breakConnection, Action1 wrapCloseInAction)
```

#### <a name="possible-reasons-and-solutions"></a>可能的原因與解決方案

- SQL Server 不支援 TLS 1.2

  此錯誤通常會在如 Docker 映像容器、Unix 用戶端或 Windows 用戶端等用戶端環境中發生，其中 TLS 1.2 是支援的最低 TLS 通訊協定。

  **建議的解決方案：** 安裝支援的 SQL Server 版本的最新更新<sup>1</sup>，並確保已在伺服器上啟用 TLS 1.2 通訊協定。

  <sup>1</sup> 請參閱 [SqlClient 驅動程式支援生命週期](sqlclient-driver-support-lifecycle.md)以取得不同版本的 Microsoft.Data.SqlClient 所支援的 SQL Server 版本清單。

  **不安全的解決方案：** 在 Docker 映像/用戶端環境上設定 TLS/SSL 設定以使用 TLS 1.0 來連線。

  ```docker
  MinProtocol = TLSv1
  CipherString = DEFAULT@SECLEVEL=1
  ```

  > [!NOTE]
  > 從 Windows/Linux 環境中搭配 TLS 1.0 或 TLS 1.1 使用 Microsoft.Data.SqlClient v2.0+ 來連線時，如果目標 SQL Server 與用戶端無法在建立連線時協調 TLS 1.2 的最低版本，系統將會擲回安全性警告訊息：`Security Warning: The negotiated <TLS1.0 | TLS1.1> is an insecure protocol and is supported for backward compatibility only. The recommended protocol version is TLS 1.2 and later.`

- SQL Server 強制加密

  如果目標伺服器是已開啟 [強制加密] 屬性的 Azure SQL 執行個體或內部部署 SQL Server，系統將會建立加密連線，且用戶端必須與伺服器建立信任。

  **建議的解決方案：** 有兩個可用的選項可修正此問題：

    1. 在用戶端環境安裝目標 SQL Server 的 TLS/SSL 憑證。 如果需要加密，系統將會加以驗證。
    2. 在連接字串設定 "Trust Server Certificate = true" 屬性。

  **不安全的解決方案：** 在 SQL Server 上停用 [強制加密] 設定。

- 未使用 SHA-256 或更高版本簽署的 TLS/SSL 憑證。

  **建議的解決方案：** 針對其雜湊是使用最新 SHA-256 雜湊演算法簽署的伺服器產生新的 TLS/SSL 憑證。

### <a name="connection-pool-exhaustion-errors"></a>連接集區耗盡錯誤

觀察到的 StackTrace：

```log
System.InvalidOperationException: Timeout expired. The timeout period elapsed prior to obtaining a connection from the pool.
This may have occurred because all pooled connections were in use and max pool size was reached.
```

#### <a name="possible-reasons-and-solutions"></a>可能的原因與解決方案

用戶端應用程式所開啟的連線數目，比起連接集區在任何時間點所能保持作用中的數目還要多。

**建議的解決方案：** 將 [集區大小上限] 連線屬性設定為較高的值，並及時關閉未使用的連線。

## <a name="contact-support"></a>請連絡支援人員

如果此指南無法解決您的連線問題，您可以檢視 [dotnet/sqlclient](https://github.com/dotnet/SqlClient) \(英文\) 存放庫中的現有問題，然後視需要提出新的問題。
