---
title: Windows 上的 ODBC Driver for SQL Server 版本資訊
ms.custom: ''
ms.date: 03/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b8459ed8-625e-4d8b-891c-e7e78c9977cc
ms.reviewer: v-chojas
author: v-makouz
ms.author: v-chojas
manager: kenvh
ms.openlocfilehash: e9210592e4c4e347662dc0ec534d511be4fa2e95
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "80345424"
---
# <a name="release-notes-for-microsoft-odbc-driver-for-sql-server-on-windows"></a>Windows 上的 Microsoft ODBC Driver for SQL Server 版本資訊

此版本資訊文章描述 Microsoft ODBC Driver to SQL Server on Windows 的最新功能。

<!--
PLEASE USE THE STANDARD 2-COLUMN TABLE FORMAT!

For all our Release Notes articles (What's New too?), we are standardizing on the 2-column format that you see here for version "## 17.3".

Going forward, all new additions to this article must use the 2-column format.

Also, use the shorter ## H2 title format, which eliminates all the redundant constants, and appends the date-added.
One beneift of shortness is the avoidance of the annoying wrapping of unnecessarily long H2 titles in the rightNav.
- OLD H2:  ## What's New in the [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.3 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] on Windows
- NEW H2:  ## 17.3, February 2019

By the way, in GitHub, the file name is changing today 2019/03/30:
- FROM:  docs/connect/odbc/windows/release-notes.md
- TO  :  docs/connect/odbc/windows/release-notes-odbc-sql-server-windows.md

Thank you.
GeneMi (and CraigG).  2019/03/30.
-->

## <a name="1752"></a>17.5.2

![下載](../../../ssms/media/download-icon.png) [下載 x64 安裝程式](https://go.microsoft.com/fwlink/?linkid=2120137)  
![下載](../../../ssms/media/download-icon.png) [下載 x86 安裝程式](https://go.microsoft.com/fwlink/?linkid=2120140)  

版本號碼：17.5.2.1  
發行日期：2019 年 3 月 6 日

如果您需要下載非所偵測語言的安裝程式，則可以使用下列直接連結。  
若為 x64 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2120137&clcid=0x40a)  
若為 x86 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2120140&clcid=0x40a)  

### <a name="features-added-in-1752"></a>在 17.5.2 版中新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| 支援使用 Azure Key Vault 受控識別進行驗證 | 請參閱[搭配 ODBC 驅動程式使用 Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md)。 |
| 支援其他的 Azure Key Vault 端點 | 請參閱[搭配 ODBC 驅動程式使用 Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md)。 |
| 錯誤修正。 | 請參閱 [Bug 修正](../bug-fixes.md)。 |
| &nbsp; | &nbsp; |

## <a name="previous-releases"></a>舊版

按一下下列各節中的下載連結來下載舊版 ODBC 驅動程式：

## <a name="175"></a>17.5

![下載](../../../ssms/media/download-icon.png) [下載 x64 安裝程式](https://go.microsoft.com/fwlink/?linkid=2120248)  
![下載](../../../ssms/media/download-icon.png) [下載 x86 安裝程式](https://go.microsoft.com/fwlink/?linkid=2120353)  

版本號碼：17.5.1.1  
發行日期：2019 年 1 月 31 日

如果您需要下載非所偵測語言的安裝程式，則可以使用下列直接連結。  
若為 x64 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2120248&clcid=0x40a)  
若為 x86 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2120353&clcid=0x40a)  

### <a name="features-added-in-175"></a>在 17.5 版中新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| SQL_COPT_SS_SPID 連線屬性，無需往返伺服器即可擷取 SPID | 請參閱 [DSN 與連接字串屬性和關鍵字](../dsn-connection-string-attribute.md)。 |
| 錯誤修正。 | 請參閱 [Bug 修正](../bug-fixes.md)。 |
| &nbsp; | &nbsp; |

## <a name="1742"></a>17.4.2

![下載](../../../ssms/media/download-icon.png) [下載 x64 安裝程式](https://go.microsoft.com/fwlink/?linkid=2120354)  
![下載](../../../ssms/media/download-icon.png) [下載 x86 安裝程式](https://go.microsoft.com/fwlink/?linkid=2120249)  

版本號碼：17.4.2.1  
發行日期：2019 年 10 月

如果您需要下載非所偵測語言的安裝程式，則可以使用下列直接連結。  
若為 x64 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2120354&clcid=0x40a)  
若為 x86 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2120249&clcid=0x40a)  

### <a name="features-added-in-1742"></a>在 17.4.2 版中新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| 支援其他的 Azure Key Vault 端點 | 請參閱[搭配 ODBC 驅動程式使用 Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md)。 |
| 支援設定資料分類版本 | 請參閱[資料分類](../data-classification.md#bkmk-version)。 |
| 在安裝程式中包含 Azure Active Directory 驗證程式庫 (adal.dll) | ODBC 安裝程式現已包含在基底驅動程式安裝中，會升級適用於 SQL Server 的 Microsoft Active Directory 驗證程式庫現有安裝，將其從 Windows 中的已安裝應用程式清單中移除。 |
| 錯誤修正。 | 請參閱 [Bug 修正](../bug-fixes.md)。 |
| &nbsp; | &nbsp; |

## <a name="174"></a>17.4

![下載](../../../ssms/media/download-icon.png) [下載 x64 安裝程式](https://go.microsoft.com/fwlink/?linkid=2120149)  
![下載](../../../ssms/media/download-icon.png) [下載 x86 安裝程式](https://go.microsoft.com/fwlink/?linkid=2120150)  

版本號碼：17.4.1.1  
發行日期：2019 年 7 月

如果您需要下載非所偵測語言的安裝程式，則可以使用下列直接連結。  
若為 x64 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2120149&clcid=0x40a)  
若為 x86 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2120150&clcid=0x40a)  

### <a name="features-added-in-174"></a>在 17.4 版中新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| 具有安全記憶體保護區的 Always Encrypted。 | 請參閱[搭配 ODBC 驅動程式使用 Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md)。 |
| 可設定的 TCP 保持連線設定。 | 請參閱[連線到 SQL Server](../linux-mac/connection-string-keywords-and-data-source-names-dsns.md)。 |
| 錯誤修正。 | 請參閱 [Bug 修正](../bug-fixes.md)。 |
| &nbsp; | &nbsp; |

## <a name="173"></a>17.3

![下載](../../../ssms/media/download-icon.png) [下載 x64 安裝程式](https://go.microsoft.com/fwlink/?linkid=2120355)  
![下載](../../../ssms/media/download-icon.png) [下載 x86 安裝程式](https://go.microsoft.com/fwlink/?linkid=2120356)  

版本號碼：17.3.1.1  
發行日期：2019 年 2 月

如果您需要下載非所偵測語言的安裝程式，則可以使用下列直接連結。  
若為 x64 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2120355&clcid=0x40a)  
若為 x86 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2120356&clcid=0x40a)  

### <a name="features-added-in-173"></a>在 17.3 版中新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| Azure Active Directory 受控服務識別 (系統和使用者指派) 驗證模式。 | 請參閱[搭配 ODBC 驅動程式使用 Azure Active Directory](../using-azure-active-directory.md)。 |
| 針對 Always Encrypted 資料行串流輸入參數的能力。 | 請參閱[使用 Always Encrypted 時的 ODBC 驅動程式限制](../using-always-encrypted-with-the-odbc-driver.md#limitations-of-the-odbc-driver-when-using-always-encrypted)。 |
| XA 分散式交易。 | [使用 XA 交易](../use-xa-with-dtc.md)。 |
| 錯誤修正。 | 請參閱 [Bug 修正](../bug-fixes.md)。 |
| &nbsp; | &nbsp; |

## <a name="172"></a>17.2

![下載](../../../ssms/media/download-icon.png) [下載 x64 安裝程式](https://go.microsoft.com/fwlink/?linkid=2120250)  
![下載](../../../ssms/media/download-icon.png) [下載 x86 安裝程式](https://go.microsoft.com/fwlink/?linkid=2120357)  

版本號碼：17.2.0.1  
發行日期：2018 年 7 月

如果您需要下載非所偵測語言的安裝程式，則可以使用下列直接連結。  
若為 x64 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2120250&clcid=0x40a)  
若為 x86 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2120357&clcid=0x40a)  

### <a name="features-added-in-172"></a>在 17.2 版中新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| 適用於 Azure SQL Database 和 SQL Server 的資料分類。 | 請參閱[資料分類](../data-classification.md)。 |
| UTF-8 伺服器編碼的支援。 | &nbsp; |
| 錯誤修正。 | 請參閱 [Bug 修正](../bug-fixes.md)。 |
| &nbsp; | &nbsp; |

## <a name="171"></a>17.1

![下載](../../../ssms/media/download-icon.png) [下載 x64 安裝程式](https://go.microsoft.com/fwlink/?linkid=2120151)  
![下載](../../../ssms/media/download-icon.png) [下載 x86 安裝程式](https://go.microsoft.com/fwlink/?linkid=2120443)  

版本號碼：17.1.0.1  
發行日期：2018 年 3 月

如果您需要下載非所偵測語言的安裝程式，則可以使用下列直接連結。  
若為 x64 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2120151&clcid=0x40a)  
若為 x86 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2120443&clcid=0x40a)  

### <a name="features-added-in-171"></a>在 17.1 版中新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| `SQL_COPT_SS_CEKCACHETTL` 和 `SQL_COPT_SS_TRUSTEDCMKPATHS` 連接屬性的支援。 | &bull; &nbsp; `SQL_COPT_SS_CEKCACHETTL`<br/>允許控制資料行加密金鑰本機快取的存在時間，以及清除它。<br/><br/>&bull; &nbsp; `SQL_COPT_SS_TRUSTEDCMKPATHS`<br/>允許應用程式限制為 AE 作業只能使用指定清單的資料行主要金鑰。<br/><br/> 如需詳細資訊，請參閱[搭配 ODBC Driver for SQL Server 使用 Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md)。 |
| Azure Active Directory 互動式驗證支援 | &nbsp; |
| 錯誤修正。 | 請參閱 [Bug 修正](../bug-fixes.md)。 |
| &nbsp; | &nbsp; |

## <a name="170"></a>17.0

![下載](../../../ssms/media/download-icon.png) [下載 x64 安裝程式](https://go.microsoft.com/fwlink/?linkid=2120444)  
![下載](../../../ssms/media/download-icon.png) [下載 x86 安裝程式](https://go.microsoft.com/fwlink/?linkid=2120152)  

版本號碼：17.0.1.1  
發行日期：2018 年 2 月

如果您需要下載非所偵測語言的安裝程式，則可以使用下列直接連結。  
若為 x64 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2120444&clcid=0x40a)  
若為 x86 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2120152&clcid=0x40a)  

### <a name="features-added-in-170"></a>在 17.0 版中新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| BCP API 的 Always Encrypted 支援。 | &nbsp; |
| 新的連接字串屬性 `UseFMTOnly`。 | 導致驅動程式在需要暫存資料表的特殊案例中使用舊版中繼資料。 |
| Azure SQL 受控執行個體的支援。 | 請參閱下列[使用受控執行個體 (ODBC 第 17 版) 時的差異](#diffs-managed-instance-17)清單。 |
| &nbsp; | &nbsp; |

| 相依性變更 | 詳細資料 |
| :------------ | :------ |
| 已移除 Microsoft Online Services 登入小幫手 | 已移除相依性。 |
| &nbsp; | &nbsp; |

### <a name="differences-when-using-managed-instance-odbc-version-17"></a><a name="diffs-managed-instance-17"></a> 使用受控執行個體 (ODBC 第 17 版) 時的差異

這個 ODBC 版本包含對 Azure SQL 受控執行個體的支援。 請參閱下列使用受控執行個體時的差異附註清單。

> [!NOTE]
> 使用受控執行個體時，有一些差異：
>
> - 不支援 FILESTREAM。
> - 不支援本機檔案系統存取，但追蹤檔案等項目需要本機檔案系統存取。
> - 不支援從本機路徑建立 UDT。
> - 不支援 Windows 整合式驗證。
> - 不支援 DTC。
> - `sa` 帳戶不存在 (預設帳戶稱為 `cloudSA`)。
> - TDS 權杖錯誤 (0xAA) 會傳回不正確的伺服器名稱。
> - 不支援在資料庫名稱中使用特殊字元。
> - 不支援 ALTER DATABASE [dbname1] MODIFY NAME = [dbname2]。
> - 錯誤訊息一律會以英文顯示，不論語言設定為何 (與 Azure 相同)。

## <a name="131"></a>13.1

![下載](../../../ssms/media/download-icon.png) [下載 x64 安裝程式](https://go.microsoft.com/fwlink/?linkid=2121020)  
![下載](../../../ssms/media/download-icon.png) [下載 x86 安裝程式](https://go.microsoft.com/fwlink/?linkid=2120923)  

版本號碼：13.1  

如果您需要下載非所偵測語言的安裝程式，則可以使用下列直接連結。  
若為 x64 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2121020&clcid=0x40a)  
若為 x86 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2120923&clcid=0x40a)  

[下載 Microsoft Command Line Utilities 13.1 for SQL Server](https://www.microsoft.com/download/details.aspx?id=53591)

### <a name="features-added-in-131"></a>在 13.1 版中新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 新增對 [Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) 和 [Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md) 的支援。 | 連線到 Microsoft SQL Server 2016 或更新版本時，可以使用這些新增的支援。 |
| 有連線集區的關鍵字和屬性，它們對應到 Always Encrypted 與 Azure Active Directory 的支援。 | 這些關鍵字和屬性，描述於 [ODBC Driver for SQL Server 中的驅動程式感知連線集區](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)。 |
| &nbsp; | &nbsp; |

## <a name="13"></a>13

![下載](../../../ssms/media/download-icon.png) [下載 x64 安裝程式](https://go.microsoft.com/fwlink/?linkid=2121118)  
![下載](../../../ssms/media/download-icon.png) [下載 x86 安裝程式](https://go.microsoft.com/fwlink/?linkid=2120924)  

版本號碼：13  

如果您需要下載非所偵測語言的安裝程式，則可以使用下列直接連結。  
若為 x64 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2121118&clcid=0x40a)  
若為 x86 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2120924&clcid=0x40a)  

[下載 Microsoft Command Line Utilities 13 for SQL Server](https://www.microsoft.com/download/details.aspx?id=52680)

### <a name="features-added-in-13"></a>在 13 版中新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| 新增對 Microsoft SQL Server 2016 的支援。 | 保留 ODBC 驅動程式第 11 版的功能。 |
| &nbsp; | &nbsp; |

## <a name="11"></a>11

![下載](../../../ssms/media/download-icon.png) [下載 x64 安裝程式](https://go.microsoft.com/fwlink/?linkid=2121206)  
![下載](../../../ssms/media/download-icon.png) [下載 x86 安裝程式](https://go.microsoft.com/fwlink/?linkid=2121021)  

版本號碼：11  

如果您需要下載非所偵測語言的安裝程式，則可以使用下列直接連結。  
若為 x64 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2121206&clcid=0x40a)  
若為 x86 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2121021&clcid=0x40a)  

[下載 Microsoft Command Line Utilities 11 for SQL Server](https://www.microsoft.com/download/details.aspx?id=36433)  

### <a name="features-added-in-11"></a>在 11 版中新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| 包含新功能。 | 請參閱 [Microsoft ODBC Driver for SQL Server on Windows 的功能](features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)。 |
| 包含 SQL Server 2012 Native Client 中 ODBC 隨附的所有功能。 | &nbsp; |
| &nbsp; | &nbsp; |
