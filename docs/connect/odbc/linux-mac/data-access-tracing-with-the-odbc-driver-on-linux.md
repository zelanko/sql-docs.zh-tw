---
title: 透過 Linux 和 macOS 上的 ODBC 驅動程式進行資料存取追蹤 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data access tracing
- tracing
ms.assetid: 3149173a-588e-47a0-9f50-edb8e9adf5e8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1fa39cd11f70a661de5c284e56f2ccc0f7a5777f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008817"
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>透過 Linux 和 macOS 上的 ODBC 驅動程式進行資料存取追蹤

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

MacOS 和 Linux 上的 unixODBC 驅動程式管理員支援對 ODBC API 呼叫進入和結束 ODBC 驅動程式[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的追蹤。

若要追蹤應用程式的 ODBC 行為, 請`odbcinst.ini`編輯檔案`[ODBC]`的區段, 將值`Trace=Yes`和`TraceFile`設定為包含追蹤輸出的檔案路徑, 例如:

```ini
[ODBC]
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```

(您也可以使用`/dev/stdout`或任何其他裝置名稱, 將追蹤輸出傳送至該處, 而不是持續性檔案)。使用上述設定, 每次應用程式載入 unixODBC 驅動程式管理員時, 它會將它執行的所有 ODBC API 通話記錄到輸出檔中。

在您完成應用程式的追蹤之後`Trace=Yes` , 請`odbcinst.ini`從檔案中移除, 以避免追蹤的效能損失, 並確保移除任何不必要的追蹤檔案。

追蹤適用於所有在 `odbcinst.ini` 中使用驅動程式的應用程式。 若不要追蹤所有的應用程式 (例如，若要避免洩漏機密的個別使用者資訊)，您可以使用 `ODBCSYSINI` 環境變數為其提供私用 `odbcinst.ini` 的位置，以追蹤個別的應用程式執行個體。 例如：

```bash
$ ODBCSYSINI=/home/myappuser myapp
```

在此情況下, 您可以`Trace=Yes`將加入`[ODBC Driver 13 for SQL Server]`至的`/home/myappuser/odbcinst.ini`區段。

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>決定驅動程式所使用的 odbc.ini 檔案

Linux 和 macOS ODBC 驅動程式不知道正在使用`odbc.ini`哪一個或檔案的路徑。 `odbc.ini` 不過, 您可以從`odbc.ini` unixODBC 工具`odbc_config`和`odbcinst`, 以及從 unixODBC 驅動程式管理員檔, 取得使用哪個檔案的相關資訊。

例如，下列命令會列印可能分別包含系統和使用者 DSN 的系統和使用者 `odbc.ini` 檔案的位置 (以及其他資訊)：

```
$ odbcinst -j
unixODBC 2.3.1
DRIVERS............: /etc/odbcinst.ini
SYSTEM DATA SOURCES: /etc/odbc.ini
FILE DATA SOURCES..: /etc/ODBCDataSources
USER DATA SOURCES..: /home/odbcuser/.odbc.ini`
SQLULEN Size.......: 8
SQLLEN Size........: 8
SQLSETPOSIROW Size.: 8
```

[UnixODBC 檔](http://www.unixodbc.org/doc/UserManual/)說明使用者與系統 dsn 之間的差異。 總結:

- 使用者 Dsn---這些是僅供特定使用者使用的 Dsn。 使用者可以使用、新增、修改及移除自己的使用者 Dsn 來進行連接。 使用者 Dsn 會儲存在使用者主目錄中的檔案, 或其子目錄。

- 系統 Dsn---這些 Dsn 可供系統上的每個使用者使用, 但只能由系統管理員新增、修改及移除。 如果使用者與系統 DSN 具有相同的名稱, 則會在該使用者連接時使用該使用者 DSN。

## <a name="see-also"></a>另請參閱

- [程式設計指導方針](../../../connect/odbc/linux-mac/programming-guidelines.md)
