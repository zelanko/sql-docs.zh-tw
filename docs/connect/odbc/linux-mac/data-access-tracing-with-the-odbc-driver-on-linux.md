---
title: 資料存取追蹤與 ODBC Driver on Linux 及 macOS |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data access tracing
- tracing
ms.assetid: 3149173a-588e-47a0-9f50-edb8e9adf5e8
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 64a04e7c448161c22ca9a671e5fdbe706829bced
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>使用 ODBC Driver on Linux 及 macOS 的資料存取追蹤
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

UnixODBC Driver Manager macOS 和 Linux 上的支援的 ODBC API 呼叫項目追蹤和結束的 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。

若要追蹤您的應用程式的 ODBC 行為，請編輯`odbcinst.ini`檔案的`[ODBC]`區段來設定的值`Trace=Yes`和`TraceFile`也就是包含在追蹤的輸出; 該檔案的路徑，例如：

```  
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```  

(您也可以使用`/dev/stdout`或任何其他裝置名稱來傳送追蹤持續性的檔案而不是那里輸出。)使用上述的設定，每次應用程式載入 unixODBC 驅動程式管理員，它會記錄它執行插入輸出檔的所有 ODBC API 呼叫。

追蹤您的應用程式完成之後，移除`Trace=Yes`從`odbcinst.ini`檔案以避免追蹤會降低效能，並確定任何不必要的追蹤檔案會遭到移除。
  
追蹤適用於所有使用中的驅動程式的應用程式`odbcinst.ini`。 不追蹤所有應用程式 （例如，若要避免洩漏機密的個別使用者資訊），您可以藉由提供它的私用位置追蹤個別應用程式執行個體`odbcinst.ini`，並使用`ODBCSYSINI`環境變數。 例如：  
  
```  
$ ODBCSYSINI=/home/myappuser myapp
```  
  
在此情況下，您可以加入`Trace=Yes`至`[ODBC Driver 13 for SQL Server]`區段`/home/myappuser/odbcinst.ini`。

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>判斷哪個 odbc.ini 檔案正在使用驅動程式

Linux 及 macOS ODBC 驅動程式不知道哪些`odbc.ini`處於使用中或路徑`odbc.ini`檔案。 不過，瞭解哪些`odbc.ini`檔案是使用可從 unixODBC 工具`odbc_config`和`odbcinst`，以及從 unixODBC 驅動程式管理員文件。  
  
例如，下列命令會列印 （以及其他資訊） 的系統和使用者位置`odbc.ini`分別包含系統和使用者名稱 （dsn） 的檔案：

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

[UnixODBC 文件](http://www.unixodbc.org/doc/UserManual/)說明使用者和系統名稱 （dsn） 之間的差異。 歸納起來：  

- 使用者名稱 （dsn）---這些是只可用為特定使用者的名稱 （dsn）。 使用者可以使用連線、 新增、 修改及移除自己的使用者名稱 （dsn）。 使用者 Dsn 會儲存在使用者的主目錄或類別的子目錄中的檔案。
  
- 系統 Dsn---這些名稱 （dsn） 可供系統上每個使用者連接使用，但可以只加入、 修改，並已由系統管理員移除。 如果使用者具有相同名稱做為系統 DSN 的使用者 DSN，將在連接時使用使用者 DSN，該使用者。

## <a name="see-also"></a>另請參閱
[程式設計指導方針](../../../connect/odbc/linux-mac/programming-guidelines.md)
