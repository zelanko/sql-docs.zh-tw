---
title: 下載 Microsoft JDBC Driver for SQL Server
description: 下載 Microsoft JDBC Driver for SQL Server 以開發連線到 SQL Server 的 Java 應用程式。
ms.date: 01/29/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 451181b8-11e6-4d01-b547-9ac5aada8238
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fcf034b332494750885d4808b54c9cb62c37077c
ms.sourcegitcommit: 4b2c9d648b7a7bdf9c3052ebfeef182e2f9d66af
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/04/2020
ms.locfileid: "77013113"
---
# <a name="download-microsoft-jdbc-driver-for-sql-server"></a>下載 Microsoft JDBC Driver for SQL Server

此文章提供 Microsoft JDBC Driver for SQL Server 的下載連結。 此驅動程式可讓您開發連線到 SQL Server 的 Java 應用程式。  

## <a name="available-downloads-of-jdbc-driver-for-sql-server"></a>JDBC Driver for SQL Server 的可用下載

使用下表中的連結來下載符合您 Java Runtime Environment (JRE) 的最新 Microsoft JDBC Driver for SQL Server：

| 版本 | 發行日期 | Java 版本 |
|---|---|---|
| [Microsoft JDBC Driver 8.2](https://go.microsoft.com/fwlink/?linkid=2116870) | 1/31/2020 | JRE 8、11、13 |
| [Microsoft JDBC Driver 7.4](https://go.microsoft.com/fwlink/?linkid=2099962) | 8/1/2019 | JRE 8、11、12 |
| [Microsoft JDBC Driver 7.2](https://go.microsoft.com/fwlink/?linkid=2063159) | 4/17/2019 | JRE 8、11 |
| [Microsoft JDBC Driver 7.0](https://go.microsoft.com/fwlink/?linkid=2005972) | 7/31/2018 | JRE 8、10 |
| [Microsoft JDBC Driver 6.4](https://go.microsoft.com/fwlink/?linkid=868290)  | 3/26/2018 | JRE 7、8、9 |
| [Microsoft JDBC Driver 6.2](https://go.microsoft.com/fwlink/?linkid=852460) | 2/12/2018 | JRE 7、8 |
| [Microsoft JDBC Driver 6.0](https://go.microsoft.com/fwlink/?LinkId=245496) | 2/27/2018 | JRE 7、8 |
| [Microsoft JDBC Driver 4.2](https://go.microsoft.com/fwlink/?linkid=841534) | 2/26/2018 | JRE 7、8 |

當您下載驅動程式時，會有多個 JAR 檔案。 JAR 檔案的名稱指出其支援的 Java 版本。 如需每個版本的詳細資訊，請參閱[版本資訊](release-notes-for-the-jdbc-driver.md)和[系統需求](system-requirements-for-the-jdbc-driver.md)。

## <a name="using-the-jdbc-driver-with-maven-central"></a>搭配 Maven Central 使用 JDBC 驅動程式

您可以使用下列程式碼來將 JDBC 驅動程式新增為 POM.xml 檔案中的相依性，藉以將該驅動程式新增至 Maven 專案：

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>8.2.0.jre11</version>
</dependency>
```  

## <a name="unsupported-drivers"></a>不支援的驅動程式

這裡不提供下載不支援的驅動程式版本。 因為我們會持續改進 Java 連線能力支援， 所以強烈建議您使用最新版的 Microsoft JDBC 驅動程式。  
  
## <a name="next-steps"></a>後續步驟

如需 Microsoft JDBC Driver for SQL Server 的詳細資訊，請參閱[JDBC 驅動程式概觀](overview-of-the-jdbc-driver.md)和[JDBC 驅動程式 GitHub 存放庫](https://github.com/microsoft/mssql-jdbc/blob/dev/README.md) \(英文\)。
