---
title: Microsoft Drivers for PHP 的版本資訊
description: 此頁面討論每版 Microsoft Drivers for PHP for SQL Server 的變更內容。
ms.custom: ''
ms.date: 09/11/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 90b9a9174f849ac8ec8cb0c1c9674395d5b38325
ms.sourcegitcommit: 780a81c02bc469c6e62a9c307e56a973239983b6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/11/2020
ms.locfileid: "90027269"
---
# <a name="release-notes-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 的版本資訊

此頁面討論每版 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 的新功能。  

<!--
Hello, We are standardizing the format of content inside our Release Notes (or What's New) articles.
Instead of bullets (or paragraphs), we have shifted to the 2-column format you see for H2 **What's New in Version 5.6**.
It is not necessary to reformat all the older H2 sections in this Release Notes file, but.....

Going forward, please be sure to use the 2-column format.

Also, all Release Notes .md file names now must begin with 'release-notes-*.md'.  And no filler words.
The 5.6 edition of this file is being renamed.....
FROM:  'release-notes-for-the-php-sql-driver.md'
TO  :  'release-notes-php-sql-driver.md'

For any questions, ask GeneMi or CraigG.
Thanks a lot.  2019-03-28  (DevO= 1467988)
-->

## <a name="581"></a>5.8.1

此版本僅適用於 Linux 和 macOS。

[GitHub 發行標記 (您可以在這裡找到 Linux 與 macOS 套件)](https://github.com/Microsoft/msphpsql/releases/tag/v5.8.1)

### <a name="version-information"></a>版本資訊

- 版本號碼：5.8.1
- 發行日期：2020 年 4 月 15 日

### <a name="whats-new-in-581"></a>5\.8.1 的新功能

| 新項目 | 詳細資料 |
| :------- | :------ |
| 錯誤 (bug) 修正 | 已修正 Alpine Linux 中的預設地區設定問題。 |
| 錯誤 (bug) 修正 | 已移除不必要的資料結構，以支援 Alpine Linux 中的用戶端資料指標功能。 |
| 錯誤 (bug) 修正 | 已修正 Alpine Linux 中同時啟用這兩個驅動程式的記錄問題。 |
| &nbsp; | &nbsp; |

## <a name="58"></a>5.8

![下載](../../ssms/media/download-icon.png) [下載 Windows 套件](https://go.microsoft.com/fwlink/?linkid=2120362)  
[GitHub 發行標記 (您可以在這裡找到 Linux 與 macOS 套件)](https://github.com/Microsoft/msphpsql/releases/tag/v5.8.0)

### <a name="version-information"></a>版本資訊

- 版本號碼：5.8.0
- 發行日期：2020 年 1 月 31 日

### <a name="whats-new-in-58"></a>5\.8 的新功能

| 新項目 | 詳細資料 |
| :------- | :------ |
| 已新增 PHP 7.4 的支援。 | &nbsp; |
| 已停止 PHP 7.1 的支援。 | &nbsp; |
| 已在所有平台上新增 Microsoft ODBC Driver 17.5 的支援。 | &nbsp; |
| 已新增 Debian 10 和 Red Hat 8 的支援。 | 兩者都需要 ODBC Driver 17.4 或更新版本。 |
| 已新增 macOS Catalina、Alpine Linux 3.11<sup>1</sup> 和 Ubuntu 19.10 的支援。 | 全部都需要 ODBC Driver 17.5 或更新版本。 |
| 已停止 SQL Server 2008 R2、macOS Sierra、Ubuntu 18.10 和 Ubuntu 19.04 的支援。 | &nbsp; |
| 當連線到 SQL Server 時，支援「語言」選項。 | &nbsp; |
| PHP 7.2 中導入 PHP 延伸字串類型的支援。 | &nbsp; |
| 「資料分類」敏感度中繼資料擷取的支援。 | 需要 SQL Server 2019 和 ODBC Driver 17.4.2 或更新版本。 |
| 具有安全記憶體保護區的 Always Encrypted 支援。 | 需要 ODBC Driver 17.4 或更新版本。 |
| Linux 與 macOS 中地區設定可設定選項的支援。 |
| 已藉由在擷取時快取中繼資料，以及忽略多餘呼叫來改善效能。 | &nbsp; |
| &nbsp; | &nbsp; |

<sup>1</sup> Alpine Linux 支援針對 5.8 版為實驗性。

## <a name="previous-releases"></a>舊版

## <a name="561"></a>5.6.1

![下載](../../ssms/media/download-icon.png) [下載 Windows 套件](https://go.microsoft.com/fwlink/?linkid=2120446)  
[GitHub 發行標記 (您可以在這裡找到 Linux 與 macOS 套件)](https://github.com/Microsoft/msphpsql/releases/tag/v5.6.1)

### <a name="version-information"></a>版本資訊

- 版本號碼：5.6.1
- 發行日期：2019 年 3 月 19 日

### <a name="whats-new-in-561"></a>5\.6.1 的新功能：

| 新項目 | 詳細資料 |
| :------- | :------ |
| 錯誤 (bug) 修正 | 已修正計算欄位或資料行中繼資料時所作的假設，這可能導致應用程式終止。 |
| 錯誤 (bug) 修正 | 已修改 sqlsrv 設定檔，使其可以獨立於 pdo_sqlsrv 之外進行編譯。 |
| 錯誤 (bug) 修正 | 已修正 PDOStatement::getColumnMeta() 以在發生錯誤時傳回 false。 |
| &nbsp; | &nbsp; |

## <a name="56"></a>5.6

![下載](../../ssms/media/download-icon.png) [下載 Windows 套件](https://go.microsoft.com/fwlink/?linkid=2120450)  
[GitHub 發行標記 (您可以在這裡找到 Linux 與 macOS 套件)](https://github.com/Microsoft/msphpsql/releases/tag/v5.6.0)

### <a name="version-information"></a>版本資訊

- 版本號碼：5.6.0
- 發行日期：2019 年 2 月 21 日

### <a name="whats-new-in-56"></a>5\.6 的新功能

| 新項目 | 詳細資料 |
| :------- | :------ |
| PHP 7.3 的支援。 | &nbsp; |
| 已停止 PHP 7.0 的支援。 | &nbsp; |
| 所有平台上 Microsoft ODBC Driver 17.3 的支援。 | &nbsp; |
| macOS Mojave 的支援。 | 需要 ODBC Driver 17.3 或更新版本。 |
| Ubuntu 18.10 和 Suse Linux 15 的支援。 | 兩者都需要 ODBC Driver 17.3 或更新版本。 |
| 已停止 Linux Ubuntu 17.10 和 macOS El Capitan 的支援。 | &nbsp; |
| Azure AD 存取權杖的支援。 | 在 Linux 和 macOS 中，需要 ODBC Driver 17.2+ 和 unixODBC 2.3.6+。 |
| 針對 Azure 資源使用受控識別對 Azure AD 進行驗證的支援。 | 需要 ODBC Driver 17.3+。 |
| 新的擷取功能 | &bull; &nbsp; pdo_sqlsrv 的新 PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE 旗標，可將日期時間作為物件傳回。<br/><br/>&bull; &nbsp; 針對 sqlsrv 將 ReturnDatesAsStrings 選項新增至陳述式層級。<br/><br/>&bull; &nbsp; 針對兩個驅動程式新增連線與陳述式層級選項，可對擷取結果中的小數值進行格式設定。 |
| 如果使用者選擇從來源建置，則支援驅動程式的靜態編譯。 | &nbsp; |
| 已藉由在擷取時快取中繼資料，以及加快 Unicode 字串轉換來改善效能。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="53"></a>5.3

![下載](../../ssms/media/download-icon.png) [下載 Windows 套件](https://go.microsoft.com/fwlink/?linkid=2120447)  
[GitHub 發行標記 (您可以在這裡找到 Linux 與 macOS 套件)](https://github.com/Microsoft/msphpsql/releases/tag/v5.3.0)

### <a name="version-information"></a>版本資訊

- 版本號碼：5.3.0
- 發行日期：2018 年 7 月 20 日

### <a name="whats-new-in-53"></a>5\.3 的新功能

- 所有平台上 Microsoft ODBC Driver 17.2 的支援
- macOS High Sierra 的支援 (需要 ODBC Driver 17 和更新版本)
- 針對基本 CRUD 功能支援適用於 Always Encrypted 的 Azure Key Vault，讓所有支援的 Windows、Linux 或 macOS 平台都能使用 Always Encrypted 功能 [搭配 PHP Drivers for SQL Server 使用 Always Encrypted](using-always-encrypted-php-drivers.md)
- 支援 Ubuntu 18.04 LTS (需要 ODBC Driver 17.2)
- Linux 以及 macOS 中連線復原的支援 (需要 ODBC Driver 17.2)

## <a name="52"></a>5.2

![下載](../../ssms/media/download-icon.png) [下載 Windows 套件](https://go.microsoft.com/fwlink/?linkid=2120451)  
[GitHub 發行標記 (您可以在這裡找到 Linux 與 macOS 套件)](https://github.com/Microsoft/msphpsql/releases/tag/v5.2.0)

### <a name="version-information"></a>版本資訊

- 版本號碼：5.2.0
- 發行日期：2018 年 3 月 23 日

### <a name="whats-new-in-52"></a>5\.2 的新功能

- Windows 上 PHP 7.2.1 和更新版本，以及其他平台上 7.2.0 和更新版本的支援
- Microsoft ODBC Driver 17 的支援
  - 17 版現在是所有平台上的預設值
- Ubuntu 17.10、Debian 9 和 Suse Enterprise Linux 12 的支援
- 已停止 Ubuntu 15.10 的支援
- Windows 上 Always Encrypted (具有 CRUD 功能) 的支援。 如需詳細資訊，請參閱[搭配 PHP Drivers for SQL Server 使用 Always Encrypted](using-always-encrypted-php-drivers.md)
  - Windows 憑證存放區的支援
  - Microsoft ODBC Driver 17 和更新版本才支援 Always Encrypted
- Linux 和 macOS 上非 UTF8 地區設定的支援
  - Microsoft ODBC Driver 17 和更新版本才支援 Linux 和 macOS 上的非 UTF8 地區設定
- Azure SQL 資料倉儲的支援
- Azure SQL 受控執行個體的支援

## <a name="43"></a>4.3

![下載](../../ssms/media/download-icon.png) [下載 Windows 套件](https://go.microsoft.com/fwlink/?linkid=2120616)  
[GitHub 發行標記 (您可以在這裡找到 Linux 與 macOS 套件)](https://github.com/Microsoft/msphpsql/releases/tag/v4.3.0)

### <a name="version-information"></a>版本資訊

- 版本號碼：4.3.0
- 發行日期：2017 年 7 月 6 日

### <a name="whats-new-in-43"></a>4\.3 的新功能

- PHP 7.1 的支援
- macOS Sierra 和 macOS El Capitan 的支援
- Ubuntu 15.10 和 Debian 8 的支援
- 已停止 Ubuntu 15.04 的支援
- 透過透明網路 IP 解析支援 Always On 可用性群組。 如需詳細資訊，請參閱 [Connection Options](connection-options.md)。
- 新增 sql_variant 資料類型有限制的支援。
- Windows 中的「閒置連線復原」功能支援。 如需詳細資訊，請參閱 [Connection Options](connection-options.md)。
- Linux 和 macOS 的連線共用支援。 如需詳細資訊，請參閱[連接共用](connection-pooling-microsoft-drivers-for-php-for-sql-server.md)。
- 使用 ActiveDirectoryPassword 和 SqlPassword 進行 Azure Active Directory 驗證的支援。 如需詳細資訊，請參閱 [Connection Options](connection-options.md)。

## <a name="40"></a>4.0

![下載](../../ssms/media/download-icon.png) [下載 Windows 套件](https://go.microsoft.com/fwlink/?linkid=2120448)  
[GitHub 發行標籤](https://github.com/microsoft/msphpsql/releases/tag/v4.0-RTW)

### <a name="version-information"></a>版本資訊

- 版本號碼：4.0
- 發行日期：2016 年 7 月 1 日

### <a name="whats-new-in-40"></a>4\.0 的新功能

- PHP 7.0 的支援  
- 完整 64 位元支援
- Ubuntu 15.04、Ubuntu 16.04 和 RedHat 7 的支援

## <a name="32"></a>3.2

![下載](../../ssms/media/download-icon.png) [下載 Windows 套件](https://go.microsoft.com/fwlink/?linkid=2120449)  
[GitHub 發行標籤](https://github.com/microsoft/msphpsql/releases/tag/v3.2.0.0)

### <a name="version-information"></a>版本資訊

- 版本號碼：3.2
- 發行日期：2015 年 3 月 9 日

### <a name="whats-new-in-32"></a>3\.2 的新功能

- PHP 5.6 的支援  
- 包含 PHP 舊有的 5.5 和 5.4 版最新的更新  
- 需要 Microsoft ODBC Driver 11 for SQL Server  

## <a name="31"></a>3.1

![下載](../../ssms/media/download-icon.png) [下載 Windows 套件](https://go.microsoft.com/fwlink/?linkid=2143027)  
[GitHub 發行標籤](https://github.com/microsoft/msphpsql/releases/tag/v3.1.0.0)

### <a name="version-information"></a>版本資訊

- 版本號碼：3.1
- 發行日期：2014 年 12 月 12 日

### <a name="whats-new-in-31"></a>3\.1 的新功能

- PHP 5.5 的支援  
- 需要 Microsoft ODBC Driver 11 for SQL Server。 舊版需要 SQL Native Client。  

## <a name="30"></a>3.0

![下載](../../ssms/media/download-icon.png) [下載 Windows 套件](https://go.microsoft.com/fwlink/?linkid=2143026)  

### <a name="whats-new-in-30"></a>3\.0 的新功能  

- PHP 5.4 的支援  [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]第 3 版不支援 PHP 5.2。  
- 已加入 AttachDBFileName 連接選項。 如需詳細資訊，請參閱 [Connection Options](connection-options.md)。  
- LocalDB 的支援，已在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中新增。 如需詳細資訊，請參閱[支援 LocalDB](php-driver-for-sql-server-support-for-localdb.md)。
- 已加入 AttachDBFileName 連接選項。 如需詳細資訊，請參閱 [Connection Options](connection-options.md)。  
- 高可用性與災害復原功能的支援。 如需詳細資訊，請參閱[對於高可用性、災害復原的支援](php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。
- 用戶端資料指標的支援 (快取記憶體中的結果集)。 如需詳細資訊，請參閱[資料指標類型 &#40;SQLSRV 驅動程式&#41;](cursor-types-sqlsrv-driver.md) 和[資料指標類型 &#40;PDO_SQLSRV 驅動程式&#41;](cursor-types-pdo-sqlsrv-driver.md)。
- 已加入 PDO::ATTR_EMULATE_PREPARES 屬性。 如需詳細資訊，請參閱 [PDO::prepare](pdo-prepare.md)。  

## <a name="20"></a>2.0

### <a name="whats-new-in-20"></a>2\.0 的新功能

在 2.0 版中，已加入對 PDO_SQLSRV 驅動程式的支援。 如需詳細資訊，請參閱 [PDO_SQLSRV 驅動程式參考](pdo-sqlsrv-driver-reference.md)。  

## <a name="see-also"></a>另請參閱

[Microsoft Drivers for PHP for SQL Server 概觀](overview-of-the-php-sql-driver.md)
