---
title: 下載 Microsoft JDBC Driver for SQL Server
description: 下載 Microsoft JDBC Driver for SQL Server 以開發連線到 SQL Server 的 Java 應用程式。
ms.date: 03/24/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 451181b8-11e6-4d01-b547-9ac5aada8238
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3f2e9f4d0c89438684201bef3bcb5d764af2cec1
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922411"
---
# <a name="download-microsoft-jdbc-driver-for-sql-server"></a>下載 Microsoft JDBC Driver for SQL Server

Microsoft JDBC Driver for SQL Server 為 Type 4 JDBC 驅動程式，透過可在 Java 平台上取得的標準 JDBC API 提供資料庫連接。 所有使用者都可免費下載驅動程式。 其可供從任何 Java 應用程式、應用程式伺服器或啟用 Java 的 Applet 存取 SQL Server。

## <a name="download"></a>下載

8\.2 版是最新的正式運作 (GA) 版本。 支援 Java 8、11 和 13。 如果需要在比該版本更舊的 Java Runtime 上執行，請參閱 [Java 及 JDBC 規格支援對照表](microsoft-jdbc-driver-for-sql-server-support-matrix.md#java-and-jdbc-specification-support)，以查看是否有支援的驅動程式版本可供使用。 我們會持續改善 Java 連線能力支援。 所以強烈建議您使用最新版的 Microsoft JDBC 驅動程式。

**[![下載](../../ssms/media/download-icon.png) 下載 Microsoft JDBC Driver 8.2 for SQL Server (zip)](https://go.microsoft.com/fwlink/?linkid=2122433)**  
**[![下載](../../ssms/media/download-icon.png) 下載 Microsoft JDBC Driver 8.2 for SQL Server (tar.gz)](https://go.microsoft.com/fwlink/?linkid=2122536)**  

### <a name="version-information"></a>版本資訊

- 版本號碼：8.2.2
- 發行日期：2020 年 3 月 24 日

當您下載驅動程式時，會有多個 JAR 檔案。 JAR 檔案的名稱指出其支援的 Java 版本。

> [!Note]
> 如果您在非英文語言版本存取此頁面，且想要查看最新內容，請參閱[本頁面的英文 (美國) 版](https://aka.ms/downloadmssqljdbcenglish)。 您可以選取[可用的語言](#available-languages)，從英文 (美國) 版網站下載不同語言版本。

## <a name="available-languages"></a>可用的語言

這一版的 Microsoft JDBC Driver for SQL Server 提供下列語言版本：

Microsoft JDBC Driver 8.2.2 for SQL Server (zip)：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x40a)

Microsoft JDBC Driver 8.2.2 for SQL Server (tar.gz)：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x40a)

### <a name="release-notes"></a>版本資訊

如需此版本的詳細資訊，請參閱[版本資訊](release-notes-for-the-jdbc-driver.md)和[系統需求](system-requirements-for-the-jdbc-driver.md)。

### <a name="previous-releases"></a>舊版

若要下載舊版，請參閱[舊版 Microsoft JDBC Driver for SQL Server](release-notes-for-the-jdbc-driver.md#previous-releases)。

## <a name="using-the-jdbc-driver-with-maven-central"></a>搭配 Maven Central 使用 JDBC 驅動程式

您可以使用下列程式碼來將 JDBC 驅動程式新增為 POM.xml 檔案中的相依性，藉以將該驅動程式新增至 Maven 專案：

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>8.2.2.jre11</version>
</dependency>
```  

## <a name="unsupported-drivers"></a>不支援的驅動程式

這裡不提供下載不支援的驅動程式版本。 因為我們會持續改進 Java 連線能力支援， 所以強烈建議您使用最新版的 Microsoft JDBC 驅動程式。  
  
## <a name="next-steps"></a>後續步驟

如需 Microsoft JDBC Driver for SQL Server 的詳細資訊，請參閱[JDBC 驅動程式概觀](overview-of-the-jdbc-driver.md)和[JDBC 驅動程式 GitHub 存放庫](https://github.com/microsoft/mssql-jdbc/blob/dev/README.md) \(英文\)。
