---
title: 版本資訊 (OLE DB Driver for SQL Server) |Microsoft Docs
ms.date: 07/03/2018
ms.prod: sql
ms.suite: sql
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
ms.openlocfilehash: ec5abfce888f0af956f1b72f509ef298ee7405a0
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2018
ms.locfileid: "39109370"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>Microsoft OLE DB Driver for SQL Server 的版本資訊
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

此頁面說明新增功能的每個版本的 Microsoft OLE DB driver for SQL Server。

## <a name="whats-new-in-version-1810"></a>18.1.0 版的新功能

**新增的功能：**

* 支援`UseFMTONLY`連接字串關鍵字和`SSPROP_INIT_USEFMTONLY`初始化屬性。
`UseFMTONLY` 控制當連接到要擷取的中繼資料的方式[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]及更新版本。  
如需詳細資訊，請參閱：
  * [利用 OLE DB Driver for SQL Server 使用連接字串關鍵字](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)

**已修正的 bug:**

* BCP 格式檔案的固定不正確的版本。 OLE DB 驅動程式 18.0 未正確設定而不是 11.0 18.0 BCP 格式檔案的版本。 OLE DB 驅動程式 18.1 無法讀取 OLE DB 驅動程式 18.0 所產生的格式檔案。 如果您需要使用舊版的 將驅動程式與新的驅動程式所產生的格式檔案，您可以手動編輯要變更的版本為 11.0 的檔案。

## <a name="whats-new-in-version-1802"></a>18.0.2 版的新功能

**新增功能**:

* 支援`MultiSubnetFailover`連接字串關鍵字和`SSPROP_INIT_MULTISUBNETFAILOVER`初始化屬性。  
如需詳細資訊，請參閱：  
  * [OLE DB Driver for SQL Server 支援高可用性、災害復原](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  
  * [利用 OLE DB Driver for SQL Server 使用連接字串關鍵字](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)

## <a name="see-also"></a>另請參閱
[Microsoft OLE DB Driver for SQL Server](oledb-driver-for-sql-server.md)
