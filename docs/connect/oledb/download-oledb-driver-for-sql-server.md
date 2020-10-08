---
title: 下載 Microsoft OLE DB Driver for SQL Server | Microsoft Docs
description: 下載 Microsoft OLE DB Driver for SQL Server，以開發連線到 SQL Server 和 Azure SQL Database 的原生 Windows 應用程式。
ms.date: 05/25/2020
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4424f11e4b8d31c964d024b3ecaf90bec0cd7c21
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727339"
---
# <a name="download-microsoft-ole-db-driver-for-sql-server"></a>下載 Microsoft OLE DB Driver for SQL Server

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

OLE DB Driver for SQL Server 是用於 OLE DB 的獨立資料存取應用程式開發介面 (API)。 OLE DB Driver for SQL Server 可在 Windows 上取得，並會在一個動態連結程式庫 (DLL) 中提供 SQL OLE DB 驅動程式。

## <a name="download"></a>下載

Microsoft OLE DB Driver for SQL Server 的可轉散發安裝程式會安裝必要的用戶端元件，以在執行階段期間使用較新的 SQL Server 功能。 從 18.3 版開始，該安裝程式也會包含並安裝 Microsoft Active Directory 驗證程式庫 (ADAL.dll)。

Microsoft OLE DB Driver 18.4 for SQL Server 是最新的正式運作 (GA) 版本。 如果已安裝舊版的 Microsoft OLE DB Driver 18 for SQL Server，則安裝 18.4 會將其升級至 18.4。

**[![下載](../../ssms/media/download-icon.png) 下載 Microsoft OLE DB Driver for SQL Server (x64)](https://go.microsoft.com/fwlink/?linkid=2129954)**  
**[![下載](../../ssms/media/download-icon.png) 下載 Microsoft OLE DB Driver for SQL Server (x86)](https://go.microsoft.com/fwlink/?linkid=2131003)**  

### <a name="version-information"></a>版本資訊

- 版本號碼：18.4.0
- 發行日期：2020 年 5 月 30 日

> [!Note]
> 如果您在非英文語言版本存取此頁面，且想要查看最新內容，請參閱[本頁面的英文 (美國) 版]()。 您可以選取[可用的語言](#available-languages)，從英文 (美國) 版網站下載不同語言版本。

## <a name="available-languages"></a>可用的語言

這一版的 Microsoft OLE DB Driver for SQL Server 可以用下列語言安裝：

Microsoft OLE DB Driver 18.4 for SQL Server (x64)：  
[簡體中文](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x40a)

Microsoft OLE DB Driver 18.4 for SQL Server (x86)：  
[簡體中文](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x804) | [繁體中文](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x404) | [英文 (美國)](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x409) | [法文](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x40c) | [德文](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x407) | [義大利文](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x410) | [日文](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x411) | [韓文](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x412) | [葡萄牙文 (巴西)](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x416) | [俄文](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x419) | [西班牙文](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x40a)

## <a name="release-notes"></a>版本資訊

如需此版本的詳細資料，請參閱[版本資訊](release-notes-for-oledb-driver-for-sql-server.md)。

## <a name="previous-releases"></a>舊版

[舊版的 Microsoft OLE DB Driver for SQL Server](release-notes-for-oledb-driver-for-sql-server.md#previous-releases)

## <a name="see-also"></a>另請參閱

[Microsoft OLE DB Driver for SQL Server 的版本資訊](release-notes-for-oledb-driver-for-sql-server.md)  
[OLE DB Driver for SQL Server 的系統需求](system-requirements-for-oledb-driver-for-sql-server.md)  
[OLE DB Driver for SQL Server 的支援原則](applications\support-policies-for-oledb-driver-for-sql-server.md)  
[使用 OLE DB Driver for SQL Server 的時機](when-to-use-oledb-driver-for-sql-server.md)  
[安裝 OLE DB Driver for SQL Server](applications/installing-oledb-driver-for-sql-server.md)