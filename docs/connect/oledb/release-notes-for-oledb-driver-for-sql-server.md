---
title: OLE DB Driver 的版本資訊
description: 此版本資訊文章描述每個 Microsoft OLE DB Driver for SQL Server 版本中的變更。
ms.date: 05/25/2020
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: 2e957fdb91720c46f5065f4b671c14b757a7cb0f
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726909"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>Microsoft OLE DB Driver for SQL Server 的版本資訊

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

此頁面討論每版 Microsoft OLE DB Driver for SQL Server 的新功能。

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

## <a name="1840"></a>18.4.0
![下載](../../ssms/media/download-icon.png) [下載 x64 安裝程式](https://go.microsoft.com/fwlink/?linkid=2129954)  
![下載](../../ssms/media/download-icon.png) [下載 x86 安裝程式](https://go.microsoft.com/fwlink/?linkid=2131003)  

發行日期：2020 年 5 月

如果您需要下載非所偵測語言的安裝程式，則可以使用下列直接連結。  
若為 x64 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x40a)  
若為 x86 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x40a)  

### <a name="features-added"></a>新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| 透明網路 IP 解析 (TNIR) 的支援 |[透明網路 IP 解析 (TNIR)](features/using-transparent-network-ip-resolution.md)|
| UTF-8 用戶端編碼的支援 | [OLE DB Driver for SQL Server 中的 UTF-8 支援](features/utf-8-support-in-oledb-driver-for-sql-server.md) |

### <a name="bugs-fixed"></a>修正的 Bug

| 已修正的錯誤 (Bug) | 詳細資料 |
| :-------- | :------ |
| 已修正 [ISequentialStream](/previous-versions/windows/desktop/ms718035(v=vs.85)) 介面中的各種 Bug | 一些影響多位元組字碼頁的 Bug 會導致此介面在讀取作業期間提前報告到達資料流結尾。|
| 已修正 [IOpenRowset::OpenRowset](/previous-versions/windows/desktop/ms716724(v=vs.85)) 介面中的記憶體流失問題 | 已修正啟用 `SSPROP_IRowsetFastLoad` 屬性時，[IOpenRowset::OpenRowset](/previous-versions/windows/desktop/ms716724(v=vs.85)) 介面中發生記憶體流失的問題。 |
| 已修正涉及 `sql_variant` 資料類型和非 ASCII 字串的案例中 Bug。 | 執行涉及 `sql_variant` 資料類型和非 ASCII 字串的特定案例可能會導致資料損毀。 如需詳細資料，請參閱：[已知問題](ole-db-data-types/ssvariant-structure.md#known-issues)。 |
| 已修正 [UDL 設定對話方塊](help-topics/data-link-pages.md)中 [測試連線] 按鈕的問題 | [UDL 設定對話方塊](help-topics/data-link-pages.md)中 [測試連線] 按鈕現在會接受 [全部] 索引標籤中設定的初始化屬性。 |
| 已修正 `SSPROP_INIT_PACKETSIZE` 屬性預設值的處理方式 | 已修正當 `SSPROP_INIT_PACKETSIZE` 屬性設定為其預設值 `0` 時所發生的未預期錯誤。 如需此屬性的詳細資料，請參閱[初始化和授權屬性](ole-db-data-source-objects/initialization-and-authorization-properties.md)。 |
| 已修正 [IBCPSession](ole-db-interfaces/ibcpsession-ole-db.md) 中的緩衝區溢位問題 | 已修正使用格式錯誤資料檔案時的緩衝區溢位問題。 |
| 已修正協助工具問題 | 已修正安裝程式 UI 及 [SQL Server 登入對話方塊](help-topics/sql-server-login-dialog.md)中的協助工具問題 (讀取內容、定位停駐點)。 |

## <a name="previous-releases"></a>舊版

## <a name="1830"></a>18.3.0

![下載](../../ssms/media/download-icon.png) [下載 x64 安裝程式](https://go.microsoft.com/fwlink/?linkid=2117515)  
![下載](../../ssms/media/download-icon.png) [下載 x86 安裝程式](https://go.microsoft.com/fwlink/?linkid=2117517)  

發行日期：2019 年 10 月

如果您需要下載非所偵測語言的安裝程式，則可以使用下列直接連結。  
若為 x64 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x40a)  
若為 x86 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x40a)  

### <a name="features-added"></a>新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| Azure Active Directory 驗證支援 (`ActiveDirectoryInteractive`、`ActiveDirectoryMSI`)。 | [使用 Azure Active Directory](features/using-azure-active-directory.md)。 |
| 在安裝程式中包含 Azure Active Directory 驗證程式庫 (adal.dll) | OLE DB 安裝程式現已包含在基底驅動程式安裝中，會升級適用於 SQL Server 的 Microsoft Active Directory 驗證程式庫現有安裝，將其從 Windows 中的已安裝應用程式清單內移除。 |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>修正的 Bug

| 已修正的錯誤 (Bug) | 詳細資料 |
| :-------- | :------ |
| 已修正 [IIndexDefinition::DropIndex](/previous-versions/windows/desktop/ms722733(v=vs.85)) \(英文\) 中的卸除索引邏輯。 | 舊版的 OLE DB 驅動程式無法在索引擁有者的結構描述識別碼和使用者識別碼不相等時卸除主索引鍵索引。 |
| &nbsp; | &nbsp; |

按一下下列各節中的下載連結，以下載舊版的 OLE DB 驅動程式：

## <a name="1823"></a>18.2.3

![下載](../../ssms/media/download-icon.png) [下載 x64 安裝程式](https://go.microsoft.com/fwlink/?linkid=2119554)  
![下載](../../ssms/media/download-icon.png) [下載 x86 安裝程式](https://go.microsoft.com/fwlink/?linkid=2119738)  

發行日期：2019 年 6 月

如果您需要下載非所偵測語言的安裝程式，則可以使用下列直接連結。  
若為 x64 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x40a)  
若為 x86 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x40a)  

### <a name="features-added-in-1823"></a>在 18.2.3 版中新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| 支援從 SQL Server 抽取式媒體進行驅動程式升級。 | 此改善可允許直接從 SQL Server 抽取式媒體進行驅動程式升級。 |
| &nbsp; | &nbsp; |

## <a name="1822"></a>18.2.2

![下載](../../ssms/media/download-icon.png) [下載 x64 安裝程式](https://go.microsoft.com/fwlink/?linkid=2118512)  
![下載](../../ssms/media/download-icon.png) [下載 x86 安裝程式](https://go.microsoft.com/fwlink/?linkid=2118415)  

發行日期：2019 年 5 月

如果您需要下載非所偵測語言的安裝程式，則可以使用下列直接連結。  
若為 x64 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x40a)  
若為 x86 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x40a)  

### <a name="bugs-fixed-in-1822"></a>在 18.2.2 中修正的 Bug

| 已修正的錯誤 (Bug) | 詳細資料 |
| :-------- | :------ |
| 修正了多執行緒 Apartment (MTA)中的非互動式 Azure Active Directory 驗證。 | OLE DB Driver 18.2.1 不當地嘗試變更先前已初始化成多執行緒 (MTA) 之 Apartment 上的 COM 並行存取模型。 如此一來，在呼叫 [idbinitialize:: Initialize](/previous-versions/windows/desktop/ms718026(v=vs.85))介面之前，先接著多次呼叫 [CoInitialize](/windows/win32/api/objbase/nf-objbase-coinitialize) 或 [CoInitializeEx](/windows/win32/api/combaseapi/nf-combaseapi-coinitializeex) 的應用程式中，無論使用何種 Azure Active Directory 驗證模式，此驅動程式均無法連線。 |
| &nbsp; | &nbsp; |

## <a name="1821"></a>18.2.1

![下載](../../ssms/media/download-icon.png) [下載 x64 安裝程式](https://go.microsoft.com/fwlink/?linkid=2118511)  
![下載](../../ssms/media/download-icon.png) [下載 x86 安裝程式](https://go.microsoft.com/fwlink/?linkid=2118278)  

發行日期：2019 年 2 月

如果您需要下載非所偵測語言的安裝程式，則可以使用下列直接連結。  
若為 x64 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x40a)  
若為 x86 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x40a)  

### <a name="features-added-in-1821"></a>在 18.2.1 版中新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| UTF-8 伺服器編碼的支援。 | [OLE DB Driver for SQL Server 中的 UTF-8 支援](features/utf-8-support-in-oledb-driver-for-sql-server.md)。 |
| Azure Active Directory 驗證支援。 | [使用 Azure Active Directory](features/using-azure-active-directory.md)。 |
| &nbsp; | &nbsp; |

## <a name="1810"></a>18.1.0

![下載](../../ssms/media/download-icon.png) [下載 x64 安裝程式](https://go.microsoft.com/fwlink/?linkid=2118506)  
![下載](../../ssms/media/download-icon.png) [下載 x86 安裝程式](https://go.microsoft.com/fwlink/?linkid=2118509)  

發行日期：2018 年 7 月

如果您需要下載非所偵測語言的安裝程式，則可以使用下列直接連結。  
若為 x64 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x40a)  
若為 x86 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2118509&2118509=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x40a)  

### <a name="features-added-in-1810"></a>在 18.1.0 版中新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| 支援 `UseFMTONLY` 連接字串關鍵字及`SSPROP_INIT_USEFMTONLY` 初始化屬性。 | `UseFMTONLY` 控制連線到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]及更新版本時，如何擷取中繼資料。<br/><br/>如需詳細資訊，請參閱[利用 OLE DB Driver for SQL Server 使用連接字串關鍵字](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。 |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed-in-1810"></a>在 18.1.0 中修正的 Bug

| 已修正的錯誤 (Bug) | 詳細資料 |
| :-------- | :------ |
| 修正了 BCP 格式檔案的不正確版本。 | OLE DB Driver 18.0 會不當地將 BCP 格式檔案設定為 18.0，而不是 11.0。<br/>OLE DB Driver 18.1 無法讀取 OLE DB Driver 18.0 產生的格式檔案。<br/>若您需要在新版驅動程式中使用舊版驅動程式產生的格式檔案，可以手動編輯該檔案，將版本變更為 11.0。 |
| &nbsp; | &nbsp; |

## <a name="1802"></a>18.0.2

![下載](../../ssms/media/download-icon.png) [下載 x64 安裝程式](https://go.microsoft.com/fwlink/?linkid=2118504)  
![下載](../../ssms/media/download-icon.png) [下載 x86 安裝程式](https://go.microsoft.com/fwlink/?linkid=2118277)  

發行日期：2018 年 3 月

如果您需要下載非所偵測語言的安裝程式，則可以使用下列直接連結。  
若為 x64 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x40a)  
若為 x86 驅動程式：[簡體中文](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x40a)  

### <a name="features-added-in-1802"></a>在 18.0.2 版中新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| 支援 `MultiSubnetFailover` 連接字串關鍵字及 `SSPROP_INIT_MULTISUBNETFAILOVER` 初始化屬性。 | 如需詳細資訊，請參閱<br/>&bull; &nbsp; [OLE DB Driver for SQL Server 高可用性和災害復原支援](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)、<br/>&bull; &nbsp; [利用 OLE DB Driver for SQL Server 使用連接字串關鍵字](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。 |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>另請參閱

[Microsoft OLE DB Driver for SQL Server](oledb-driver-for-sql-server.md)