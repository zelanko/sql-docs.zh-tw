---
title: 版本資訊 (OLE DB Driver for SQL Server) | Microsoft Docs
ms.date: 10/11/2019
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: 350856cc27bdec601e0db2998f9ff9953cdf6ec7
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381726"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>Microsoft OLE DB Driver for SQL Server 的版本資訊

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

此頁面討論每版 Microsoft OLE DB Driver for SQL Server 的新功能。

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

## <a name="1830"></a>18.3.0

2019 年 10 月

### <a name="features-added"></a>新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| Azure Active Directory 驗證支援 (`ActiveDirectoryInteractive`、`ActiveDirectoryMSI`)。 | [使用 Azure Active Directory](features/using-azure-active-directory.md)。 |
| 支援內嵌 Active Directory 驗證程式庫（ADAL）。 | 不需要另外安裝 ADAL，即可使用特定的驗證方法。 |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>修正的 Bug

| 已修正的錯誤 (Bug) | 詳細資料 |
| :-------- | :------ |
| 已修正 IIndexDefinition 中的 drop index 邏輯[：:D ropindex](https://go.microsoft.com/fwlink/?linkid=2106448)。 | 當索引擁有者的架構識別碼和使用者識別碼不相等時，舊版的 OLE DB 驅動程式無法卸載主鍵索引。 |
| &nbsp; | &nbsp; |

## <a name="1823"></a>18.2.3

2019 年 6 月

### <a name="features-added"></a>新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| 支援從 SQL Server 卸載式媒體升級驅動程式。 | 這種改善可直接從 SQL Server 卸載式媒體升級驅動程式。 |
| &nbsp; | &nbsp; |

## <a name="1822"></a>18.2.2

2019 年 5 月

### <a name="bugs-fixed"></a>修正的 Bug

| 已修正的錯誤 (Bug) | 詳細資料 |
| :-------- | :------ |
| 修正了多執行緒 Apartment (MTA)中的非互動式 Azure Active Directory 驗證。 | OLE DB Driver 18.2.1 不當地嘗試變更先前已初始化成多執行緒 (MTA) 之 Apartment 上的 COM 並行存取模型。 如此一來，在呼叫 [idbinitialize:: Initialize](https://go.microsoft.com/fwlink/?linkid=2092522)介面之前，先接著多次呼叫 [CoInitialize](https://go.microsoft.com/fwlink/?linkid=2092520) 或 [CoInitializeEx](https://go.microsoft.com/fwlink/?linkid=2092521) 的應用程式中，無論使用何種 Azure Active Directory 驗證模式，此驅動程式均無法連線。 |
| &nbsp; | &nbsp; |

## <a name="1821"></a>18.2.1

2019 年 2 月

### <a name="features-added"></a>新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| UTF-8 伺服器編碼的支援。 | [OLE DB Driver for SQL Server 中的 UTF-8 支援](features/utf-8-support-in-oledb-driver-for-sql-server.md)。 |
| Azure Active Directory 驗證支援。 | [使用 Azure Active Directory](features/using-azure-active-directory.md)。 |
| &nbsp; | &nbsp; |

## <a name="1810"></a>18.1.0

2018 年 7 月

### <a name="features-added"></a>新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| 支援 `UseFMTONLY` 連接字串關鍵字及`SSPROP_INIT_USEFMTONLY` 初始化屬性。 | `UseFMTONLY` 控制連線到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]及更新版本時，如何擷取中繼資料。<br/><br/>如需詳細資訊，請參閱：搭配[使用連接字串關鍵字與 OLE DB Driver for SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。 |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>修正的 Bug

| 已修正的錯誤 (Bug) | 詳細資料 |
| :-------- | :------ |
| 修正了 BCP 格式檔案的不正確版本。 | OLE DB Driver 18.0 會不當地將 BCP 格式檔案設定為 18.0，而不是 11.0。<br/>OLE DB Driver 18.1 無法讀取 OLE DB Driver 18.0 產生的格式檔案。<br/>若您需要在新版驅動程式中使用舊版驅動程式產生的格式檔案，可以手動編輯該檔案，將版本變更為 11.0。 |
| &nbsp; | &nbsp; |

## <a name="1802"></a>18.0.2

### <a name="features-added"></a>新增的功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| 支援 `MultiSubnetFailover` 連接字串關鍵字及 `SSPROP_INIT_MULTISUBNETFAILOVER` 初始化屬性。 | 如需詳細資訊，請參閱：<br/>&bull; &nbsp; [OLE DB Driver for SQL Server 高可用性和災害復原支援](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)、<br/>&bull; &nbsp; [ OLE DB Driver for SQL Server 使用連接字串關鍵字](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。 |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>另請參閱

[Microsoft OLE DB Driver for SQL Server](oledb-driver-for-sql-server.md)
