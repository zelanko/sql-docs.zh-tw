---
title: 安裝 Microsoft ODBC Driver for SQL Server (macOS)
description: 了解如何在 macOS 用戶端上安裝 Microsoft ODBC Driver for SQL Server，以啟用資料庫連線能力。
ms.date: 03/05/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver, installing
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9daa17d8619fa05ac9abf52a768740eb3e223c77
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488516"
---
# <a name="install-the-microsoft-odbc-driver-for-sql-server-macos"></a>安裝 Microsoft ODBC Driver for SQL Server (macOS)

本文說明如何在 macOS 上安裝 Microsoft ODBC Driver for SQL Server， 以及如何使用適用於 SQL Server (`bcp` 和 `sqlcmd`) 與 unixODBC 開發標頭的選擇性命令列工具。

本文提供從 Bash Shell 安裝 ODBC 驅動程式的命令。 如果想要直接下載套件，請參閱[下載 ODBC Driver for SQL Server](../download-odbc-driver-for-sql-server.md)。

## <a name="microsoft-odbc-17"></a>Microsoft ODBC 17

若要在 macOS 上安裝 Microsoft ODBC Driver 17 for SQL Server，請執行下列命令：

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
HOMEBREW_NO_ENV_FILTERING=1 ACCEPT_EULA=Y brew install msodbcsql17 mssql-tools
```

> [!IMPORTANT]
> 如果您已安裝短暫提供的第 17 版 `msodbcsql` 套件，您應該先移除它，再安裝 `msodbcsql17` 套件。 如此可避免衝突。 `msodbcsql17` 套件可以和 `msodbcsql` 第 13 版套件並存安裝。

## <a name="previous-versions"></a>舊版

下列各節提供在 macOS 上安裝舊版 Microsoft ODBC 驅動程式的指示。

## <a name="odbc-131"></a><a id="13.1"></a> ODBC 13.1

使用下列命令，在 OS X 10.11 (El Capitan) 與 macOS 10.12 (Sierra) 上安裝 Microsoft ODBC driver 13.1 for SQL Server：

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install msodbcsql@13.1.9.2 mssql-tools@14.0.6.0
```

## <a name="driver-files"></a>驅動程式檔案

macOS 上的 ODBC 驅動程式包含下列元件：

|元件|描述|  
|---------------|-----------------|  
|libmsodbcsql.17.dylib 或 libmsodbcsql.13.dylib|動態連結程式庫 (`dylib`) 檔案，其中包含驅動程式的所有功能。 這個檔案會安裝在 `/usr/local/lib/`。|  
|`msodbcsqlr17.rll` 或 `msodbcsqlr13.rll`|隨附驅動程式程式庫的資源檔。 針對 Driver 17，這個檔案會安裝在 `[driver .dylib directory]../share/msodbcsql17/resources/en_US/`，針對 Driver 13 則在 `[driver .dylib directory]../share/msodbcsql/resources/en_US/`。 | 
|msodbcsql.h|標頭檔，其中包含使用驅動程式所需的所有新定義。<br /><br /> **注意：** 您無法在同一個程式中參考 msodbcsql.h 和 odbcss.h。<br /><br /> 針對 Driver 17，msodbcsql.h 會安裝在 `/usr/local/include/msodbcsql17/`，針對 Driver 13 則在 `/usr/local/include/msodbcsql/`。 |
|LICENSE.txt|文字檔案，其中包含授權條款。 針對 Driver 17，這個檔案會放在 `/usr/local/share/doc/msodbcsql17/`，針對 Driver 13 則在 `/usr/local/share/doc/msodbcsql/`。 |
|RELEASE_NOTES|文字檔案，其中包含版本資訊。 針對 Driver 17，這個檔案會放在 `/usr/local/share/doc/msodbcsql17/`，針對 Driver 13 則在 `/usr/local/share/doc/msodbcsql/`。 |

## <a name="resource-file-loading"></a>載入資源檔

驅動程式需要載入資源檔，才能運作。 這個檔案稱為 `msodbcsqlr17.rll` 或 `msodbcsqlr13.rll`，視驅動程式版本而定。 `.rll` 檔案的位置是相對於驅動程式本身 (`so` 或 `dylib`) 的位置，如上表所述。 到 17.1 版為止，驅動程式也會嘗試從預設目錄載入 `.rll`，如果從相對路徑載入失敗的話。 macOS 上的預設資源檔路徑為 `/usr/local/share/msodbcsql17/resources/en_US/`

## <a name="troubleshooting"></a>疑難排解

如果無法使用 ODBC 驅動程式建立與 SQL Server 的連線，請參閱已知問題一文中的[針對連線問題進行疑難排解](known-issues-in-this-version-of-the-driver.md#connectivity)。

## <a name="next-steps"></a>後續步驟

在安裝驅動程式後，即可嘗試使用 [C++ ODBC 範例應用程式](../../odbc/cpp-code-example-app-connect-access-sql-db.md)。 如需開發 ODBC 應用程式的詳細資訊，請參閱[開發應用程式](../../../odbc/reference/develop-app/developing-applications.md)。

如需詳細資訊，請參閱 ODBC 驅動程式的[版本資訊](release-notes-odbc-sql-server-linux-mac.md)與[系統需求](system-requirements.md)。
