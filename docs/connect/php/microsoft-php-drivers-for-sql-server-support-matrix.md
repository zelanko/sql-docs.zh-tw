---
title: Microsoft Drivers for PHP for SQL Server 支援對照表 |Microsoft Docs
ms.custom: ''
ms.date: 07/20/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
manager: ''
ms.openlocfilehash: 82a8576365889d02381e3b18b622fd541b5b9235
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47728696"
---
# <a name="microsoft-php-drivers-for-sql-server-support-matrix"></a>Microsoft PHP Drivers for SQL Server 支援對照表
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

  此頁面包含 Microsoft PHP Drivers for SQL Server 的支援對照表與支援週期原則。

## <a name="microsoft-php-drivers-support-lifecycle-matrix-and-policy"></a>Microsoft PHP 驅動程式支援生命週期對照表及原則
 Microsoft 支援週期 (MSL) 原則為 Microsoft 產品的支援生命週期提供透明而可預測的資訊。 JDBC 驅動程式 3.0、4.x、6.x 和 7.x 版自發行日期起提供五年的主要支援。 主要支援會在 [Microsoft 支援週期網站](https://support.microsoft.com/lifecycle)上定義。

 Microsoft PHP Driver 不提供延長支援與自訂支援選項。

 下列 Microsoft PHP Driver 的支援期限到指定的結束支援日期為止。

|驅動程式名稱|驅動程式套件版本|結束主要支援|
|-|-|-|
|Microsoft PHP Driver for SQL Server 5.3|5.3|2023 年 7 月 20 日|
|Microsoft PHP Driver for SQL Server 5.2|5.2|2017 年 2 月 9 日|
|Microsoft PHP Driver for SQL Server 4.3|4.3|2022 年 7 月 6 日|
|Microsoft PHP Driver 4.0 for SQL Server|4.0|2021 年 7 月 11 日|
|Microsoft PHP Drivers 3.2 for SQL Server|3.2|2020 年 3 月 9日日|
|Microsoft PHP Drivers 3.1 for SQL Server|3.1|2019 年 12 月 12 日|

 下列是不再支援的 Microsoft PHP Driver。

|驅動程式名稱|驅動程式套件版本|結束主要支援|
|-|-|-|
|Microsoft PHP Drivers 3.0 for SQL Server|3.0|2017 年 3 月 6 日|
|Microsoft PHP Drivers 2.0 for SQL Server|2.0|2015 年 8 月 10日日|
|Microsoft PHP Driver 1.0 for SQL Server|1.0|2014 年 4 月 28 日|

## <a name="sql-server-version-certified-compatibility"></a>認證的相容性的 SQL Server 版本
 下列矩陣列出測試和認證，與對應的驅動程式版本相容的 SQL Server 版本。 我們致力於維持回溯相容性與舊的驅動程式版本，但僅最新支援的驅動程式測試和認證使用新的 SQL Server 版本的 SQL Server 是發行。

|PHP for SQL Server 驅動程式版本&#8594;<br />&#8595; SQL Server 版本|5.3 和 5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|Azure SQL 受控執行個體<br/> （延伸私人預覽）|Y|Y| | | | | |
|Azure SQL 資料倉儲|Y|Y| | | | | |
|SQL Server 2017   |Y|Y| | | | | |
|SQL Server 2016   |Y|Y|Y| | | | |
|SQL Server 2014   |Y|Y|Y|Y|Y| | |
|SQL Server 2012   |Y|Y|Y|Y|Y|Y| |
|SQL Server 2008 R2|Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2008   | | |Y|Y|Y|Y|Y|

## <a name="php-version-support"></a>PHP 版本支援
 支援下列版本的 PHP 的 Microsoft PHP Drivers 列出的版本：

|PHP for SQL Server 驅動程式版本&#8594;<br />&#8595; PHP 版本|5.3 和 5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|7.2|Windows 上的 7.2.1+<br/>其他平台上的 7.2.0+| | | | | | |
|7.1|7.1.0+ |7.1.0+ |       |        |        |        |        |
|7.0|7.0.0+ |7.0.0+ |7.0.0+ |        |        |        |        |
|5.6|       |       |       |5.6.4 +  |        |        |        |
|5.5|       |       |       |5.5.16 + |5.5.16 + |        |        |
|5.4|       |       |       |5.4.32  |5.4.32  |5.4.32  |        |
|5.3|       |       |       |        |        |5.3.0   |5.3.0   |
|5.2|       |       |       |        |        |        |5.2.4<br />5.2.13|

## <a name="supported-operating-systems"></a>支援的作業系統
 下列 Windows 作業系統版本支援的 Microsoft PHP Drivers 列出的版本：

|PHP for SQL Server 驅動程式版本&#8594;<br />&#8595; 作業系統|5.3 和 5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|Windows Server 2016                 |Y  |Y  |   |   |   |   |   |
|Windows Server 2012 R2              |Y  |Y  |Y  |Y  |Y  |   |   |
|Windows Server 2012                 |Y  |Y  |Y  |Y  |Y  |   |   |
|Windows Server 2008 R2 SP1          |   |   |Y  |Y  |Y  |Y  |   |
|Windows Server 2008 R2              |   |   |   |   |   |   |Y  |
|Windows Server 2008 SP2             |   |   |Y  |Y  |Y  |Y  |   |
|Windows Server 2008                 |   |   |   |   |   |   |Y  |
|Windows Server 2003 SP1             |   |   |   |   |   |   |Y  |
|Windows 10                          |Y  |Y  |Y  |   |   |   |   |
|Windows 8.1                         |Y  |Y  |Y  |Y  |Y  |   |   |
|Windows 8                           |   |Y  |Y  |Y  |Y  |   |   |
|Windows 7 SP1                       |   |   |Y  |Y  |Y  |Y  |   |
|Windows Vista SP2                   |   |   |Y  |Y  |Y  |Y  |Y  |
|Windows XP SP3                      |   |   |   |   |   |   |Y  |

 Microsoft PHP drivers 列出的版本支援下列 Linux 和 Mac 作業系統版本 （限 64 位元）：

|PHP for SQL Server 驅動程式版本&#8594;<br />&#8595; 作業系統|5.3<br />&nbsp;|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|--|---|---|---|---|---|---|---|---|
|Ubuntu 18.04 （64 位元）               |Y  |   |   |   |   |   |   |   |
|Ubuntu 17.10 （64 位元）               |Y  |Y  |   |   |   |   |   |   |
|Ubuntu 16.04 （64 位元）               |Y  |Y  |Y  |Y  |   |   |   |   |
|Ubuntu 15.10 （64 位元）               |   |   |Y  |   |   |   |   |   |
|Ubuntu 15.04 （64 位元）               |   |   |   |Y  |   |   |   |   |
|Debian 9 （64 位元）                   |Y  |Y  |   |   |   |   |   |   |
|Debian 8 （64 位元）                   |Y  |Y  |Y  |   |   |   |   |   |
|Red Hat Enterprise Linux 7 (64 位元) |Y  |Y  |Y  |Y  |   |   |   |   |
|Suse Enterprise Linux 12 （64 位元）   |Y  |Y  |   |   |   |   |   |   |
|macOS High Sierra （64 位元）          |Y  |   |   |   |   |   |   |   |
|macOS Sierra （64 位元）               |Y  |Y  |Y  |   |   |   |   |   |
|macOS El Capitan （64 位元）           |Y  |Y  |Y  |   |   |   |   |   |

## <a name="see-also"></a>另請參閱  
[版本資訊](../../connect/php/release-notes-for-the-php-sql-driver.md)

[支援資源](../../connect/php/support-resources-for-the-php-sql-driver.md)

[系統需求](../../connect/php/system-requirements-for-the-php-sql-driver.md)
