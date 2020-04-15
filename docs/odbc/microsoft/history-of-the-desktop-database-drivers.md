---
title: 桌面資料庫驅動程式的歷史記錄 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], history
- ODBC desktop database drivers [ODBC], history
- desktop database drivers [ODBC], history
ms.assetid: b4a2aff8-bde7-4bd5-8580-bc50f27311c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89434b397c07fdee751ca4272b65ac2eada94cf3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304979"
---
# <a name="history-of-the-desktop-database-drivers"></a>桌面資料庫驅動程式歷程記錄
下表顯示了桌面資料庫驅動程式版本歷史記錄。  
  
|版本|發行日期|描述|  
|-------------|------------------|-----------------|  
|1.0|1993年8月|使用了 PageAhead 軟體生成的 SIMBA 查詢處理器。 SIMBA 接收了 ODBC 呼叫和 SQL 語句,將它們處理到 Microsoft Jet 可安裝的 ISAM 調用中,然後調用 Microsoft Jet ISAM 調度層來載入並調用適當的可安裝 ISAM 驅動程式。|  
|2.0|1994年12月|與 ODBC 2.0 一起使用,顯著擴展了 ODBC 功能。 版本 2.0 的主要變化是 Microsoft Jet 資料庫引擎取代了 SIMBA 查詢處理器。 借助 Microsoft Jet 資料庫引擎,桌面資料庫驅動程式與 Microsoft Jet 可安裝的 ISAM 驅動程式和 Microsoft Access 技術整合得更緊密。 顯著增強::<br /><br /> - 對可滾動游標的本機支援。<br />- 對外部聯接的本機支援、可異構聯接和事務。<br />- 微軟 Windows NT 的驅動程式的 32 位元版本。|  
|3.0|1995年10月|為 Windows 95 和 Windows NT 工作站或 NT 伺服器 3.51 提供支援。 此版本中僅包含 32 位元驅動程式;Windows 版本 3.1 的 16 位驅動程式已被刪除。|  
|3.5|1996年10月|這些驅動程式支援雙位元位元集 (DBCS),與以前的版本更適合 Internet 應用程式使用,並且適合使用檔案數據來源名稱 (DSN)。 Microsoft Access 驅動程式以 RISC 版本發表,用於適用於 Windows 95/98 和 Windows NT 3.51 及更高版本的作業系統的 Alpha 平臺。|  
|4.0|1998年末|支援 Microsoft 噴氣引擎 Unicode 格式以及早期版本的 ANSI 格式的相容性。|  
  
> [!NOTE]  
>  版本3.5驅動程式的設計與ODBC2配合使用。*x*. . 雖然它們也使用ODBC 3.0,但它們不支援所有ODBC 3.0功能。 有關這些驅動程式如何與 ODBC 3.0 配合使用的詳細資訊,請參閱[向後相容性和標準合規性](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。
