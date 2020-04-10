---
title: Microsoft JDBC Driver for SQL Server 支援對照表
ms.custom: ''
ms.date: 03/24/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c5769e67-99f7-4bc1-a4fa-8941dad33d35
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7f9482c80d3ea84b814857433f6ff2a0389cc544
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922837"
---
# <a name="microsoft-jdbc-driver-for-sql-server-support-matrix"></a>Microsoft JDBC Driver for SQL Server 支援對照表

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  此頁面包含 Microsoft JDBC Driver for SQL Server 的支援對照表與支援週期原則。  
  
## <a name="microsoft-jdbc-driver-support-lifecycle-matrix-and-policy"></a>Microsoft JDBC Driver 支援生命週期對照表及原則  

Microsoft 支援週期 (MSL) 原則為 Microsoft 產品的支援生命週期提供透明而可預測的資訊。 JDBC 驅動程式 3.0、4.x、6.x、7.x 和 8.x 版自驅動程式發行日期起提供五年的主要支援。 主要支援定義在 Microsoft 支援生命週期網站上。  
  
Microsoft JDBC Driver 不提供延長支援與自訂支援選項。  

下列 Microsoft JDBC Driver 的支援期限到指定的的結束支援日期為止。  
  
|驅動程式名稱|驅動程式套件版本|適用的 JAR|主要支援結束日期|
|-|-|-|-|  
|Microsoft JDBC Driver 8.2 for SQL Server|8.2|mssql-jdbc-8.2.2.jre13.jar<br> mssql-jdbc-8.2.2.jre11.jar<br> mssql-jdbc-8.2.2.jre8.jar|2025 年 3 月 24 日|
|Microsoft JDBC Driver 7.4 for SQL Server|7.4|mssql-jdbc-7.4.1.jre12.jar<br> mssql-jdbc-7.4.1.jre11.jar<br> mssql-jdbc-7.4.1.jre8.jar|2024 年 8 月 2 日|
|Microsoft JDBC Driver 7.2 for SQL Server|7.2|mssql-jdbc-7.2.2.jre11.jar<br> mssql-jdbc-7.2.2.jre8.jar|2024 年 4 月 16 日|
|Microsoft JDBC Driver 7.0 for SQL Server|7.0|mssql-jdbc-7.0.0.jre10.jar<br> mssql-jdbc-7.0.0.jre8.jar|2023 年 7 月 31 日|
|Microsoft JDBC Driver 6.4 for SQL Server|6.4|mssql-jdbc-6.4.0.jre9.jar<br> mssql-jdbc-6.4.0.jre8.jar<br> mssql-jdbc-6.4.0.jre7.jar|2023 年 2 月 27 日|
|Microsoft JDBC Driver 6.2 for SQL Server|6.2|mssql-jdbc-6.2.2.jre8.jar<br> mssql-jdbc-6.2.2.jre7.jar|2022 年 6 月 30 日|
|Microsoft JDBC Driver 6.0 for SQL Server|6.0|sqljdbc42.jar<br>sqljdbc41.jar|2021 年 7 月 14 日|
|Microsoft JDBC Driver 4.2 for SQL Server|4.2|sqljdbc42.jar<br>sqljdbc41.jar|2020 年 8 月 24 日|
  
 下列 Microsoft JDBC Driver 不再支援。  

|驅動程式名稱|驅動程式套件版本|主要支援結束日期|  
|-|-|-|
|Microsoft JDBC Driver 4.1 for SQL Server|4.1|2019 年 12 月 12 日|  
|Microsoft JDBC Driver 4.0 for SQL Server|4.0|2017 年 3 月 6 日|  
|Microsoft SQL Server JDBC Driver 3.0|3.0|2015 年 4 月 23 日|  
|Microsoft SQL Server JDBC Driver 2.0|2.0|2012 年 12 月 31 日|  
|Microsoft SQL Server 2005 JDBC Driver 1.2|1.2|2011 年 6 月 25 日|  
|Microsoft SQL Server 2005 JDBC Driver 1.1|1.1|2011 年 6 月 25 日|  
|Microsoft SQL Server 2005 JDBC Driver 1.0|1.0|2011 年 6 月 25 日|  
|Microsoft SQL Server 2000 JDBC Driver|2000|2010 年 7 月 9 日|  
  
## <a name="sql-version-compatibility"></a>SQL 的版本相容性  
  
|驅動程式版本|SQL Server 2008|SQL Server 2008R2|SQL Server 2012|Azure SQL Database|PDW 2008R2 AU3<sup>4</sup>|SQL Server 2014|SQL Server 2016|SQL Server 2017|SQL Server 2019|  
|-|-|-|-|-|-|-|-|-|-|-|
|8.2|N|N|Y|Y|Y|Y|Y|Y|Y|
|7.4|N|N|Y|Y|Y|Y|Y|Y|Y|
|7.2|N|Y|Y|Y|Y|Y|Y|Y|N|
|7.0|N|Y|Y|Y|Y|Y|Y|Y|N|
|6.4|N|Y|Y|Y|Y|Y|Y|Y|N|
|6.2|Y|Y|Y|Y|Y|Y|Y|Y|N|
|6.1|Y|Y|Y|Y|Y|Y|Y|N|N|
|6.0|Y|Y|Y|Y|Y|Y|Y|N|N|
|4.2|Y|Y|Y|Y|Y|Y|Y|N|N|
|4.1|Y|Y|Y|Y|Y|Y|Y|N|N|
|4.0|Y|Y|Y|Y|Y|Y|Y|N|N|
|3.0|Y|Y|Y<sup>1</sup>|Y<sup>2</sup>|N|Y<sup>5</sup>|N|N|N|
|2.0|Y<sup>3</sup>|Y<sup>3</sup>|N|N|N|N|N|N|N|
|1.2|Y<sup>3</sup>|N|N|N|N|N|N|N|N|
|1.1|N|N|N|N|N|N|N|N|N|
|1.0|N|N|N|N|N|N|N|N|N|
|2000|N|N|N|N|N|N|N|N|N|
  
 <sup>1</sup>Microsoft SQL Server JDBC Driver 3.0 版可用下層用戶端的身分連線到 SQL Server 2012。  
  
 <sup>2</sup>Azure SQL Database 支援在驅動程式 3.0 版中以 Hotfix 的形式推出。 建議 Azure SQL Database 客戶使用所提供的最新版驅動程式。  
  
 <sup>3</sup>Microsoft SQL Server JDBC Driver 2.0 版與 Microsoft SQL Server 2005 JDBC Driver 1.2 版可用下層用戶端的身分連線到 SQL Server 2008。 若允許轉換成下層，應用程式便能對 SQL Server 2008 資料類型 (例如 time、date、datetime2、datetimeoffset 及 FILESTREAM) 執行查詢及更新。 如需如何使用搭配使用這些新資料類型與 JDBC 驅動程式的詳細資訊，請參閱  [Working with SQL Server 2008 Date/Time Data Types using JDBC Driver](https://go.microsoft.com/fwlink/?LinkId=145198) (使用 JDBC 驅動程式時使用 SQL Server 2008 Date/Time 資料類型) 及  [Working with SQL Server 2008 FileStream using JDBC Driver](https://go.microsoft.com/fwlink/?LinkId=145199)(使用 JDBC 驅動程式時使用 SQL Server 2008 FileStream)。 如需新資料類型與下層之相容性的詳細資訊，請參閱《SQL Server 線上叢書》中的  [使用日期和時間資料](https://go.microsoft.com/fwlink/?LinkId=145211)及  [FILESTREAM 支援](https://go.microsoft.com/fwlink/?LinkId=145212) 主題。  
  
 <sup>4</sup>Microsoft JDBC Driver 與平行資料倉儲之間的連線支援首次推出於 Microsoft JDBC Driver 4.0 for SQL Server 及 Microsoft SQL Server 2008 R2 平行處理資料倉儲設備更新 3 中。  
  
 <sup>5</sup>Microsoft SQL Server JDBC Driver 3.0 版可用下層用戶端的身分連線到 SQL Server 2014。  
  
## <a name="java-and-jdbc-specification-support"></a>Java 及 JDBC 規格支援
  
|JDBC 驅動程式版本|JRE 版本|JDBC API 版本|
|-|-|-|
|[8.2](release-notes-for-the-jdbc-driver.md#82)|1.8、11、13|4.2、4.3 (部份)|
|[7.4](release-notes-for-the-jdbc-driver.md#74)|1.8、11、12|4.2、4.3 (部份)|
|[7.2](release-notes-for-the-jdbc-driver.md#72)|1.8、11|4.2、4.3 (部份)|
|[7.0](release-notes-for-the-jdbc-driver.md#70)|1.8、10|4.2、4.3 (部份)|
|[6.4](release-notes-for-the-jdbc-driver.md#64)|1.7、1.8、9|4.1、4.2、4.3 (部份)|
|[6.2](release-notes-for-the-jdbc-driver.md#62)|1.7、1.8|4.1、4.2|
|[6.1](release-notes-for-the-jdbc-driver.md#61)|1.7、1.8|4.1、4.2|
|[6.0](release-notes-for-the-jdbc-driver.md#60)|1.7、1.8|4.1、4.2|
|[4.2](release-notes-for-the-jdbc-driver.md#42)|1.7、1.8|4.1、4.2|
|4.1|1.7|4.0|
|4.0|1.5、1.6、1.7|3.0、4.0|
|3.0|1.5、1.6、|3.0、4.0|
|2.0|1.5、1.6|3.0、4.0|
|1.2|1.4、1.5、1.6|3.0|
|1.1|1.4|3.0|
|1.0|1.4|3.0|
|2000|1.4|3.0|

## <a name="supported-operating-systems"></a>支援的作業系統

Microsoft JDBC Driver 的設計可以在所有支援 JAVA 虛擬機器 (JVM) 的作業系統上運作。 一些常用的平台包括 Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Server 2008 R2、Windows Vista、Linux、Unix、AIX、macOS 等等。  

JDBC 產品小組在 Windows、Sun Solaris、SUSE Linux、Ubuntu Linux、CentOS Linux 及 macOS 上測試過我們的驅動程式。

## <a name="application-server-support"></a>應用程式伺服器支援

Microsoft JDBC Driver for SQL Server 已在各種應用程式伺服器上經過測試。  如需產品相容之驅動程式版本的詳細資訊，請洽詢您的應用程式伺服器廠商。
