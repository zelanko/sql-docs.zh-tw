---
title: Microsoft Drivers for PHP 支援矩陣
description: 此頁面包含 Microsoft PHP Drivers for SQL Server 的支援對照表與支援週期原則。
ms.custom: ''
ms.date: 04/15/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 635c6ecbe6404b7e5466ecf5929dd2330183e7a0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85793151"
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
|Microsoft PHP Drivers 5.8 for SQL Server|5.8|2025 年 1 月 31 日|
|Microsoft PHP Drivers 5.6 for SQL Server|5.6|2024 年 2 月 21 日|
|Microsoft PHP Drivers 5.3 for SQL Server|5.3|2023 年 7 月 20 日|
|Microsoft PHP Drivers 5.2 for SQL Server|5.2|2023 年 2 月 9 日|
|Microsoft PHP Drivers 4.3 for SQL Server|4.3|2022 年 7 月 6 日|
|Microsoft PHP Drivers 4.0 for SQL Server|4.0|2021 年 7 月 11 日|
|Microsoft PHP Drivers 3.2 for SQL Server|3.2|2020 年 3 月 9 日|
| &nbsp; | &nbsp; | &nbsp; |

下列是不再支援的 Microsoft PHP Driver。

|驅動程式名稱|驅動程式套件版本|主要支援結束日期|
|-|:-:|-|
|Microsoft PHP Drivers 3.1 for SQL Server|3.1|2019 年 12 月 12 日|
|Microsoft PHP Drivers 3.0 for SQL Server|3.0|2017 年 3 月 6 日|
|Microsoft PHP Drivers 2.0 for SQL Server|2.0|2015 年 8 月 10 日|
|Microsoft PHP Drivers 1.0 for SQL Server|1.0|2014 年 4 月 28 日|
| &nbsp; | &nbsp; | &nbsp; |

## <a name="sql-server-version-certified-compatibility"></a>SQL Server 版本認證相容性
 下列對照表會列出已經過測試並認證為與相對應驅動程式版本相容的 SQL Server 版本。 我們致力於維護與先前驅動程式版本之間的回溯相容性，但隨著 SQL Server 的發行，我們只會搭配新的 SQL Server 版本測試及認證最新支援的驅動程式。

|適用於 SQL Server 的 PHP 驅動程式版本 &#8594;<br />&#8595; SQL Server 版本|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Azure SQL 受控執行個體|Y|Y|Y|Y|Y| | |
|Azure SQL 資料倉儲|Y|Y|Y|Y|Y| | |
|SQL Server 2019         |Y| | | | | | |
|SQL Server 2017         |Y|Y|Y|Y|Y| | |
|SQL Server 2016         |Y|Y|Y|Y|Y|Y| |
|SQL Server 2014         |Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2012         |Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2008 R2      | |Y|Y|Y|Y|Y|Y|
|SQL Server 2008         | | | | | |Y|Y|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

## <a name="php-version-support"></a>PHP 版本支援

下列版本的 PHP 支援搭配所列出版本的 Microsoft PHP 驅動程式使用：

|適用於 SQL Server 的 PHP 驅動程式版本 &#8594;<br />&#8595; PHP 版本|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|:---:|---|---|---|---|---|---|---|
|7.4|7.4.0+          |                |                |                |       |        |        |
|7.3|7.3.0+          |7.3.0+          |                |                |       |        |        |
|7.2|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>|       |        |        |
|7.1|                |7.1.0+          |7.1.0+          |7.1.0+          |7.1.0+ |        |        |
|7.0|                |                |7.0.0+          |7.0.0+          |7.0.0+ |7.0.0+  |        |
|5.6|                |                |                |                |       |        |5.6.4+  |
|5.5|                |                |                |                |       |        |5.5.16+ |
|5.4|                |                |                |                |       |        |5.4.32  |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

1. Windows 支援 7.2.1 版及更新版本，而 Linux 及 macOS 則支援 7.2.0 版及更新版本。

## <a name="supported-operating-systems"></a>支援的作業系統

下列 Windows 作業系統版本支援搭配所列出版本的 Microsoft PHP 驅動程式使用：

|適用於 SQL Server 的 PHP 驅動程式版本 &#8594;<br />&#8595; 作業系統|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Windows Server 2019                 |Y  |Y  |   |   |   |   |   |
|Windows Server 2016                 |Y  |Y  |Y  |Y  |Y  |   |   |
|Windows Server 2012 R2              |Y  |Y  |Y  |Y  |Y  |Y  |Y  |
|Windows Server 2012                 |Y  |Y  |Y  |Y  |Y  |Y  |Y  |
|Windows Server 2008 R2 SP1          |   |   |   |   |   |Y  |Y  |
|Windows Server 2008 R2              |   |   |   |   |   |   |   |
|Windows Server 2008 SP2             |   |   |   |   |   |Y  |Y  |
|Windows 10                          |Y  |Y  |Y  |Y  |Y  |Y  |   |
|Windows 8.1                         |Y  |Y  |Y  |Y  |Y  |Y  |Y  |
|Windows 8                           |   |   |   |   |Y  |Y  |Y  |
|Windows 7 SP1                       |   |   |   |   |   |Y  |Y  |
|Windows Vista SP2                   |   |   |   |   |   |Y  |Y  |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

下列 Linux 和 macOS 作業系統版本 (僅限 64 位元) 支援搭配所列出版本的 Microsoft PHP 驅動程式使用：

|適用於 SQL Server 的 PHP 驅動程式版本 &#8594;<br />&#8595; 作業系統|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|--|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Ubuntu 19.10 (64 位元)               |Y  |   |   |   |   |   |   |
|Ubuntu 18.10 (64 位元)               |   |Y  |   |   |   |   |   |
|Ubuntu 18.04 (64 位元)               |Y  |Y  |Y  |   |   |   |   |
|Ubuntu 17.10 (64 位元)               |   |   |Y  |Y  |   |   |   |
|Ubuntu 16.04 (64 位元)               |Y  |Y  |Y  |Y  |Y  |Y  |   |
|Ubuntu 15.10 (64 位元)               |   |   |   |   |Y  |   |   |
|Ubuntu 15.04 (64 位元)               |   |   |   |   |   |Y  |   |
|Debian 10 (64 位元)                  |Y  |   |   |   |   |   |   |
|Debian 9 (64 位元)                   |Y  |Y  |Y  |Y  |   |   |   |
|Debian 8 (64 位元)                   |Y  |Y  |Y  |Y  |Y  |   |   |
|Red Hat Enterprise Linux 8 (64 位元) |Y  |   |   |   |   |   |   |
|Red Hat Enterprise Linux 7 (64 位元) |Y  |Y  |Y  |Y  |Y  |Y  |   |
|Suse Enterprise Linux 15 (64 位元)   |Y  |Y  |   |   |   |   |   |
|Suse Enterprise Linux 12 (64 位元)   |Y  |Y  |Y  |Y  |   |   |   |
|Alpine Linux 3.11 (64 位元)<sup>1</sup>|Y  |   |   |   |   |   |   |
|macOS Catalina (64 位元)             |Y  |   |   |   |   |   |   |
|macOS Mojave (64 位元)               |Y  |Y  |   |   |   |   |   |
|macOS High Sierra (64 位元)          |Y  |Y  |Y  |   |   |   |   |
|macOS Sierra (64 位元)               |   |Y  |Y  |Y  |Y  |   |   |
|macOS El Capitan (64 位元)           |   |   |Y  |Y  |Y  |   |   |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

<sup>1</sup> Alpine Linux 支援針對 5.8.0 版為實驗性。 版本 5.8.1 引進了生產環境支援。

## <a name="see-also"></a>另請參閱

[版本資訊](release-notes-php-sql-driver.md)

[支援資源](support-resources-for-the-php-sql-driver.md)

[系統需求](system-requirements-for-the-php-sql-driver.md)
