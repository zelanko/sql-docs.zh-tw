---
title: Microsoft Drivers for PHP for SQL Server 支援矩陣 |Microsoft 文件
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
caps.latest.revision: 1
author: David-Engel
ms.author: v-daveng
manager: ''
ms.openlocfilehash: b8f1fad66e906b71ff5ea247ba4615e7be774f63
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-php-drivers-for-sql-server-support-matrix"></a>Microsoft PHP 驅動程式供 SQL Server 支援對照表
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

  此頁面包含 Microsoft PHP Driver for SQL Server 支援對照表與支援週期原則。

## <a name="microsoft-php-drivers-support-lifecycle-matrix-and-policy"></a>Microsoft PHP 驅動程式支援生命週期對照表及原則
 Microsoft 支援週期 (MSL) 原則為 Microsoft 產品的支援生命週期提供透明而可預測的資訊。 3.x、 4.x，與 5.x 有五年的驅動程式的發行日期起的主要支援的 PHP 驅動程式版本。 主要支援定義於[Microsoft 支援週期網站](https://support.microsoft.com/lifecycle)。

 擴充和自訂支援選項不適用於 Microsoft PHP 驅動程式。

 支援下列的 Microsoft PHP Driver，直到指定的支援結束日期。

|驅動程式名稱|驅動程式套件版本|結束主流支援|
|-|-|-|
|SQL Server 的 Microsoft PHP 驅動程式 5.2|5.2|2023 年 2 月 9 日|
|SQL Server 的 Microsoft PHP 驅動程式 4.3|4.3|2022 年 7 月 6 日|
|Microsoft PHP 驅動程式 4.0 for SQL Server|4.0|2021 年 7 月 11 日|
|Microsoft PHP Drivers 3.2 for SQL Server|3.2|2020 年 3 月 9 日|
|Microsoft PHP Drivers 3.1 for SQL Server|3.1|2019 年 12 月 12 日|

 下列的 Microsoft PHP Driver 不再支援。

|驅動程式名稱|驅動程式套件版本|結束主流支援|
|-|-|-|
|Microsoft PHP Drivers 3.0 for SQL Server|3.0|2017 年 3 月 6 日|
|SQL Server 的 Microsoft PHP 驅動程式 2.0|2.0|2015 年 8 月 10日日|
|SQL Server 的 Microsoft PHP 驅動程式 1.0|1.0|2014 年 4 月 28日日|

## <a name="sql-server-version-certified-compatibility"></a>SQL Server 版本通過相容性
 下列矩陣會列出已測試與認證與對應的驅動程式版本相容的 SQL Server 版本。 我們致力於維護回溯相容性之前的驅動程式版本，但只有最新支援的驅動程式會測試及認證使用新的 SQL Server 版本中，SQL Server 會在釋放。

|PHP for SQL Server 驅動程式版本&#8594;<br />&#8595;SQL Server 版本|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|SQL azure 受管理的執行個體<br/> （延伸私人預覽中）|Y|Y| | | | | |
|Azure SQL 資料倉儲|Y|Y| | | | | |
|SQL Server 2017   |Y|Y| | | | | |
|SQL Server 2016   |Y|Y|Y| | | | |
|SQL Server 2014   |Y|Y|Y|Y|Y| | |
|SQL Server 2012   |Y|Y|Y|Y|Y|Y| |
|SQL Server 2008 R2|Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2008   | | |Y|Y|Y|Y|Y|

## <a name="php-version-support"></a>PHP 版本支援
 下列版本的 PHP 支援與列出的 Microsoft PHP Driver 版本：

|PHP for SQL Server 驅動程式版本&#8594;<br />&#8595;PHP 版本|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|7.2|在 Windows 上 7.2.1+<br/>在其他平台上 7.2.0+| | | | | | |
|7.1|7.1.0+ |7.1.0+ |       |        |        |        |        |
|7.0|7.0.0+ |7.0.0+ |7.0.0+ |        |        |        |        |
|5.6|       |       |       |5.6.4+  |        |        |        |
|5.5|       |       |       |5.5.16+ |5.5.16+ |        |        |
|5.4|       |       |       |5.4.32  |5.4.32  |5.4.32  |        |
|5.3|       |       |       |        |        |5.3.0   |5.3.0   |
|5.2|       |       |       |        |        |        |5.2.4<br />5.2.13|

## <a name="supported-operating-systems"></a>支援的作業系統
 列出的版本的 Microsoft PHP 驅動程式支援下列 Windows 作業系統版本：

|PHP for SQL Server 驅動程式版本&#8594;<br />&#8595;作業系統|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
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

 列出的版本的 Microsoft PHP 驅動程式支援下列 Linux 和 Mac 作業系統系統版本 （僅限 64 位元）：

|PHP for SQL Server 驅動程式版本&#8594;<br />&#8595;作業系統|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|3.0<br />&nbsp;|2.0<br />&nbsp;|
|---|---|---|---|---|---|---|---|
|Ubuntu 17.10 （64 位元）               |Y  |   |   |   |   |   |   |
|Ubuntu 16.04 （64 位元）               |Y  |Y  |Y  |   |   |   |   |
|Ubuntu 15.10 （64 位元）               |   |Y  |   |   |   |   |   |
|Ubuntu 15.04 （64 位元）               |   |   |Y  |   |   |   |   |
|Debian 9 （64 位元）                   |Y  |   |   |   |   |   |   |
|Debian 8 （64 位元）                   |Y  |Y  |   |   |   |   |   |
|Red Hat Enterprise Linux 7 （64 位元） |Y  |Y  |Y  |   |   |   |   |
|Suse Enterprise Linux 12 （64 位元）   |Y  |   |   |   |   |   |   |
|macOS 利也 （64 位元）               |Y  |Y  |   |   |   |   |   |
|macOS El Capitan （64 位元）           |Y  |Y  |   |   |   |   |   |

## <a name="see-also"></a>另請參閱  
[版本資訊](../../connect/php/release-notes-for-the-php-sql-driver.md)

[支援資源](../../connect/php/support-resources-for-the-php-sql-driver.md)

[系統需求](../../connect/php/system-requirements-for-the-php-sql-driver.md)
