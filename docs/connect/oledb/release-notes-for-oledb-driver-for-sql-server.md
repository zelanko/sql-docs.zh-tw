---
title: 版本資訊 (OLE DB Driver for SQL Server) | Microsoft Docs
ms.date: 02/13/2019
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: 2a1d6d216f4f7ec7fee0f5f9aa5810c78f1936e6
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161765"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>Microsoft OLE DB Driver for SQL Server 的版本資訊

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

此頁面說明新增功能的每個版本的 Microsoft OLE DB driver for SQL Server。

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

## <a name="1821"></a>18.2.1

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

2019 年 2 月

### <a name="features-added"></a>新增功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| Utf-8 伺服器版本編碼方式的支援。 | &bull; &nbsp; [OLE DB Driver for SQL Server 中的 UTF-8 支援](features/utf-8-support-in-oledb-driver-for-sql-server.md)。 |
| Azure Active Directory 驗證支援。 | &bull; &nbsp; [使用 Azure Active Directory](features/using-azure-active-directory.md)。 |
| &nbsp; | &nbsp; |

## <a name="1810"></a>18.1.0

2018 年 7 月

### <a name="features-added"></a>新增功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| 支援`UseFMTONLY`連接字串關鍵字，以及`SSPROP_INIT_USEFMTONLY`初始化屬性。 | `UseFMTONLY` 控制當連接到要擷取的中繼資料的方式[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]及更新版本。<br/><br/>&bull; &nbsp; [ OLE DB Driver for SQL Server 使用連接字串關鍵字](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。 |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>已修正的 bug

| 已修正的錯誤 (Bug) | 詳細資料 |
| :-------- | :------ |
| BCP 格式檔案的固定不正確的版本。 | OLE DB 驅動程式 18.0 不正確會設定而不是 18.0，BCP 格式檔案的版本為 11.0。<br/><br/>OLE DB 驅動程式 18.1 無法讀取 OLE DB 驅動程式 18.0 所產生的格式檔案。<br/><br/>如果您需要使用舊版的 將驅動程式與新的驅動程式所產生的格式檔案，您可以手動編輯要變更的版本為 11.0 的檔案。 |
| &nbsp; | &nbsp; |

## <a name="1802"></a>18.0.2

### <a name="features-added"></a>新增功能

| 新增功能 | 詳細資料 |
| :------------ | :------ |
| 支援`MultiSubnetFailover`連接字串關鍵字和`SSPROP_INIT_MULTISUBNETFAILOVER`初始化屬性。 | &bull; &nbsp; [OLE DB Driver for SQL Server 高可用性和災害復原支援](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。<br/><br/>&bull; &nbsp; [ OLE DB Driver for SQL Server 使用連接字串關鍵字](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。 |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>另請參閱

[Microsoft OLE DB Driver for SQL Server](oledb-driver-for-sql-server.md)
