---
title: Microsoft Drivers for PHP for SQL Server 支援對照表 |Microsoft Docs
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: genemi
manager: ''
ms.openlocfilehash: 0790d2cc0497ef2912f96cd4679e4541fc9b2262
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63180268"
---
# <a name="microsoft-php-drivers-for-sql-server-support-matrix"></a>Microsoft PHP Drivers for SQL Server 支援對照表

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

此頁面包含 Microsoft PHP Drivers for SQL Server 的支援對照表與支援週期原則。

## <a name="microsoft-php-drivers-support-lifecycle-matrix-and-policy"></a>Microsoft PHP 驅動程式支援生命週期對照表及原則

Microsoft 支援週期 (MSL) 原則為 Microsoft 產品的支援生命週期提供透明而可預測的資訊。 PHP 驅動程式 3.x、4.x 和 5.x 版自驅動程式發行日期起提供五年的主要支援。 主要支援會在 [Microsoft 支援週期網站](https://support.microsoft.com/lifecycle)上定義。

Microsoft PHP Driver 不提供延長支援與自訂支援選項。

下列 Microsoft PHP Driver 的支援期限到指定的結束支援日期為止。

|驅動程式名稱|驅動程式套件版本|主要支援結束日期|
|-|:-:|-|
|Microsoft PHP Drivers 5.6 for SQL Server|5.6|2024 年 2 月 21 日|
|Microsoft PHP Drivers 5.3 for SQL Server|5.3|2023 年 7 月 20 日|
|Microsoft PHP Drivers 5.2 for SQL Server|5.2|2023 年 2 月 9 日|
|Microsoft PHP Drivers 4.3 for SQL Server|4.3|2022 年 7 月 6 日|
|Microsoft PHP Drivers 4.0 for SQL Server|4.0|2021 年 7 月 11 日|
|Microsoft PHP Drivers 3.2 for SQL Server|3.2|2020 年 3 月 9日日|
|Microsoft PHP Drivers 3.1 for SQL Server|3.1|2019 年 12 月 12 日|
| &nbsp; | &nbsp; | &nbsp; |

下列是不再支援的 Microsoft PHP Driver。

|驅動程式名稱|驅動程式套件版本|主要支援結束日期|
|-|:-:|-|
|Microsoft PHP Drivers 3.0 for SQL Server|3.0|2017 年 3 月 6 日|
|Microsoft PHP Drivers 2.0 for SQL Server|2.0|2015 年 8 月 10日日|
|Microsoft PHP Drivers 1.0 for SQL Server|1.0|2014 年 4 月 28 日|
| &nbsp; | &nbsp; | &nbsp; |

## <a name="sql-server-version-certified-compatibility"></a>認證的相容性的 SQL Server 版本
 下列矩陣列出測試和認證，與對應的驅動程式版本相容的 SQL Server 版本。 我們致力於維持回溯相容性與舊的驅動程式版本，但僅最新支援的驅動程式測試和認證使用新的 SQL Server 版本的 SQL Server 是發行。

|PHP for SQL Server 驅動程式版本&#8594;<br />&#8595; SQL Server 版本|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Azure SQL 受控執行個體<br/> (延伸的個人預覽版)|Y|Y|Y|Y| | | | | |
|Azure SQL 資料倉儲|Y|Y|Y|Y| | | | | |
|SQL Server 2017         |Y|Y|Y|Y| | | | | |
|SQL Server 2016         |Y|Y|Y|Y|Y| | | | |
|SQL Server 2014         |Y|Y|Y|Y|Y|Y|Y| | |
|SQL Server 2012         |Y|Y|Y|Y|Y|Y|Y|Y| |
|SQL Server 2008 R2      |Y|Y|Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2008         | | | | |Y|Y|Y|Y|Y|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

## <a name="php-version-support"></a>PHP 版本支援

支援下列版本的 PHP 的 Microsoft PHP Drivers 列出的版本：

|PHP for SQL Server 驅動程式版本&#8594;<br />&#8595; PHP 版本|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|:---:|---|---|---|---|---|---|---|---|---|
|7.3|7.3.0+          |                |                |       |       | | | | |
|7.2|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>|       |       | | | | |
|7.1|7.1.0+          |7.1.0+          |7.1.0+          |7.1.0+ |       |        |        |        |        |
|7.0|                |7.0.0+          |7.0.0+          |7.0.0+ |7.0.0+ |        |        |        |        |
|5.6|                |                |                |       |       |5.6.4+  |        |        |        |
|5.5|                |                |                |       |       |5.5.16+ |5.5.16+ |        |        |
|5.4|                |                |                |       |       |5.4.32  |5.4.32  |5.4.32  |        |
|5.3|                |                |                |       |       |        |        |5.3.0   |5.3.0   |
|5.2|                |                |                |       |       |        |        |        |5.2.4<br />5.2.13|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

1. 7.2.1 版本和更新版本才支援在 Windows，而版本 7.2.0 和更新版本才支援在 Linux 和 macOS 上。

## <a name="supported-operating-systems"></a>支援的作業系統

下列 Windows 作業系統版本支援的 Microsoft PHP Drivers 列出的版本：

|PHP for SQL Server 驅動程式版本&#8594;<br />&#8595; 作業系統|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Windows Server 2016                 |Y  |Y  |Y  |Y  |   |   |   |   |   |
|Windows Server 2012 R2              |Y  |Y  |Y  |Y  |Y  |Y  |Y  |   |   |
|Windows Server 2012                 |Y  |Y  |Y  |Y  |Y  |Y  |Y  |   |   |
|Windows Server 2008 R2 SP1          |   |   |   |   |Y  |Y  |Y  |Y  |   |
|Windows Server 2008 R2              |   |   |   |   |   |   |   |   |Y  |
|Windows Server 2008 SP2             |   |   |   |   |Y  |Y  |Y  |Y  |   |
|Windows Server 2008                 |   |   |   |   |   |   |   |   |Y  |
|Windows Server 2003 SP1             |   |   |   |   |   |   |   |   |Y  |
|Windows 10                          |Y  |Y  |Y  |Y  |Y  |   |   |   |   |
|Windows 8.1                         |Y  |Y  |Y  |Y  |Y  |Y  |Y  |   |   |
|Windows 8                           |   |   |   |Y  |Y  |Y  |Y  |   |   |
|Windows 7 SP1                       |   |   |   |   |Y  |Y  |Y  |Y  |   |
|Windows Vista SP2                   |   |   |   |   |Y  |Y  |Y  |Y  |Y  |
|Windows XP SP3                      |   |   |   |   |   |   |   |   |Y  |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

Microsoft PHP drivers 列出的版本支援下列 Linux 和 Mac 作業系統版本 （限 64 位元）：

|PHP for SQL Server 驅動程式版本&#8594;<br />&#8595; 作業系統|5.6|5.3|5.2|4.3|4.0|3.2|3.1|3.0|2.0|
|--|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Ubuntu 18.10 （64 位元）               |Y  |   |   |   |   |   |   |   |   |
|Ubuntu 18.04 （64 位元）               |Y  |Y  |   |   |   |   |   |   |   |
|Ubuntu 17.10 （64 位元）               |   |Y  |Y  |   |   |   |   |   |   |
|Ubuntu 16.04 （64 位元）               |Y  |Y  |Y  |Y  |Y  |   |   |   |   |
|Ubuntu 15.10 （64 位元）               |   |   |   |Y  |   |   |   |   |   |
|Ubuntu 15.04 （64 位元）               |   |   |   |   |Y  |   |   |   |   |
|Debian 9 （64 位元）                   |Y  |Y  |Y  |   |   |   |   |   |   |
|Debian 8 （64 位元）                   |Y  |Y  |Y  |Y  |   |   |   |   |   |
|Red Hat Enterprise Linux 7 (64 位元) |Y  |Y  |Y  |Y  |Y  |   |   |   |   |
|Suse Enterprise Linux 15 （64 位元）   |Y  |   |   |   |   |   |   |   |   |
|Suse Enterprise Linux 12 （64 位元）   |Y  |Y  |Y  |   |   |   |   |   |   |
|macOS Mojave （64 位元）               |Y  |   |   |   |   |   |   |   |   |
|macOS High Sierra （64 位元）          |Y  |Y  |   |   |   |   |   |   |   |
|macOS Sierra （64 位元）               |Y  |Y  |Y  |Y  |   |   |   |   |   |
|macOS El Capitan （64 位元）           |   |Y  |Y  |Y  |   |   |   |   |   |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

## <a name="see-also"></a>另請參閱

[版本資訊](../../connect/php/release-notes-php-sql-driver.md)

[支援資源](../../connect/php/support-resources-for-the-php-sql-driver.md)

[系統需求](../../connect/php/system-requirements-for-the-php-sql-driver.md)
