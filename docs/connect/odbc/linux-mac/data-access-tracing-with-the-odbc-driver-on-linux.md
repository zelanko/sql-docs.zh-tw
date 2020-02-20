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
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "68008817"
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>透過 Linux 和 macOS 上的 ODBC 驅動程式進行資料存取追蹤

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

macOS 和 Linux 上的 unixODBC Driver Manager 支援針對 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 追蹤 ODBC API 呼叫的進入與結束。

若要追蹤應用程式的 ODBC 行為，請編輯 `odbcinst.ini` 檔案的 `[ODBC]` 區段，將 `Trace=Yes` 和 `TraceFile` 值設定為要包含追蹤輸出之檔案的路徑；例如：

```ini
[ODBC]
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```

(您也可以使用 `/dev/stdout` 或任何其他裝置名稱，在該處傳送追蹤輸出，而不是傳送到永續性檔案)。使用上述設定，每次應用程式載入 unixODBC Driver Manager 時，即會將其執行的所有 ODBC API 呼叫記錄到輸出檔案中。

完成應用程式的追蹤之後，請從 `odbcinst.ini` 檔案中移除 `Trace=Yes`，以避免追蹤效能受到影響，並確認已移除所有不必要的追蹤檔案。

追蹤適用於所有在 `odbcinst.ini` 中使用驅動程式的應用程式。 若不要追蹤所有的應用程式 (例如，若要避免洩漏機密的個別使用者資訊)，您可以使用 `ODBCSYSINI` 環境變數為其提供私用 `odbcinst.ini` 的位置，以追蹤個別的應用程式執行個體。 例如：

```bash
$ ODBCSYSINI=/home/myappuser myapp
```

在此案例中，您可以將 `Trace=Yes` 新增至 `/home/myappuser/odbcinst.ini` 的 `[ODBC Driver 13 for SQL Server]` 區段。

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>決定驅動程式所使用的 odbc.ini 檔案

Linux 和 macOS ODBC 驅動程式不知道正在使用哪一個 `odbc.ini`，或 `odbc.ini` 檔案的路徑。 不過，關於正在使用哪一個 `odbc.ini` 檔案的資訊可以從 unixODBC 工具 `odbc_config` 和 `odbcinst` 中取得，以及從 unixODBC Driver Manager 文件中取得。

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

[unixODBC 文件](http://www.unixodbc.org/doc/UserManual/)說明使用者與系統 DSN 之間的差異。 摘要說明：

- 使用者 DSN：這些是僅供特定使用者使用的 DSN。 使用者可以使用、新增、修改及移除自己的使用者 DSN 來連線。 使用者 DSN 會儲存於使用者主目錄或其子目錄中的檔案。

- 系統 DSN：這些 DSN 可供系統上的每個使用者用來連線，但只能由系統管理員新增、修改及移除。 如果使用者具備的使用者 DSN 與系統 DSN 具有相同名稱，則會在該使用者連線時使用使用者 DSN。

## <a name="see-also"></a>另請參閱

- [程式設計指導方針](../../../connect/odbc/linux-mac/programming-guidelines.md)
