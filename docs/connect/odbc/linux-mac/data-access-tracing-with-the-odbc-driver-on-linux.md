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
manager: jroth
ms.openlocfilehash: cd71429e5a407e595cc3f65e73e984bfc12280b1
ms.sourcegitcommit: 5d27fb187006e676d652884f0c1f5133a1bd62b2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2019
ms.locfileid: "67152215"
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>透過 Linux 和 macOS 上的 ODBC 驅動程式進行資料存取追蹤

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

在 macOS 和 Linux 的 unixODBC 驅動程式管理員支援的 ODBC API 呼叫項目追蹤和結束的 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。

若要追蹤您的應用程式的 ODBC 行為，請編輯`odbcinst.ini`檔案的`[ODBC]`一節，以設定值`Trace=Yes`和`TraceFile`也就是包含輸出; 追蹤檔案的路徑，例如：

```ini
[ODBC]
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```

(您也可以使用`/dev/stdout`或任何其他裝置名稱來傳送追蹤的持續性的檔案而不是那里輸出。)使用上述設定中，每次應用程式載入 unixODBC 驅動程式管理員 中，它會記錄它執行插入輸出檔的所有 ODBC API 呼叫。

追蹤您的應用程式完成之後，移除`Trace=Yes`從`odbcinst.ini`檔案以避免追蹤功能，對效能造成負面影響，並確認已移除任何不必要的追蹤檔案。

追蹤適用於所有在 `odbcinst.ini` 中使用驅動程式的應用程式。 若不要追蹤所有的應用程式 (例如，若要避免洩漏機密的個別使用者資訊)，您可以使用 `ODBCSYSINI` 環境變數為其提供私用 `odbcinst.ini` 的位置，以追蹤個別的應用程式執行個體。 例如：

```bash
$ ODBCSYSINI=/home/myappuser myapp
```

在此情況下，您可以在其中加入`Trace=Yes`要`[ODBC Driver 13 for SQL Server]`一節`/home/myappuser/odbcinst.ini`。

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>決定驅動程式所使用的 odbc.ini 檔案

Linux 和 macOS 的 ODBC 驅動程式不知道哪個`odbc.ini`處於使用中或路徑`odbc.ini`檔案。 不過，瞭解哪些`odbc.ini`檔案是使用可從 unixODBC 工具`odbc_config`和`odbcinst`，以及從 unixODBC 驅動程式管理員文件。

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

[UnixODBC 文件](http://www.unixodbc.org/doc/UserManual/)說明使用者和系統名稱 （dsn） 之間的差異。 在 摘要：

- 使用者名稱 （dsn）---這些是只可以使用哪些特定的使用者名稱 （dsn）。 使用者可以使用連線、 新增、 修改及移除他們自己的使用者名稱 （dsn）。 使用者 Dsn 會儲存在使用者的主目錄或類別的子目錄中的檔案。

- 系統名稱 （dsn）---這些名稱 （dsn） 可供連線使用它們，每位使用者在系統上，但只能加入、 修改和移除系統管理員。 如果使用者具有系統 DSN 名稱相同的使用者 DSN，將在連接時使用使用者 DSN，由該使用者。

## <a name="see-also"></a>另請參閱

- [程式設計指導方針](../../../connect/odbc/linux-mac/programming-guidelines.md)
