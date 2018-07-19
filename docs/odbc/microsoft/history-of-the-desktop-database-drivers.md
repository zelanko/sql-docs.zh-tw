---
title: 桌面資料庫驅動程式的歷程記錄 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], history
- ODBC desktop database drivers [ODBC], history
- desktop database drivers [ODBC], history
ms.assetid: b4a2aff8-bde7-4bd5-8580-bc50f27311c8
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 44d0dd0c1f460bbed2b256d89bb9e986764b5256
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32902233"
---
# <a name="history-of-the-desktop-database-drivers"></a>桌面資料庫驅動程式的歷程記錄
下表顯示桌面資料庫驅動程式版本歷程記錄。  
  
|版本|發行日期|Description|  
|-------------|------------------|-----------------|  
|1.0|1993 年 8 月|使用所產生的 PageAhead 軟體 SIMBA 查詢處理器。 SIMBA 收到呼叫 ODBC 和 SQL 陳述式、 執行 Microsoft Jet 可安裝 ISAM 呼叫處理它們，然後呼叫 Microsoft Jet ISAM 分派圖層以載入並呼叫適當的可安裝 ISAM 驅動程式。|  
|2.0|1994 年 12 月|搭配 ODBC 2.0，大幅擴充 ODBC 功能。 2.0 版的重大變更是 Microsoft Jet 資料庫引擎取代 SIMBA 查詢處理器。 使用 Microsoft Jet 資料庫引擎，桌面資料庫驅動程式更緊密地整合 Microsoft Jet 可安裝 ISAM 驅動程式與 Microsoft 存取技術。 已大幅增強功能：<br /><br /> -原生支援可捲動資料指標。<br />-原生支援外部聯結、 更新和異質聯結和交易。<br />-32 位元版本的 Microsoft Windows NT 的驅動程式。|  
|3.0|1995 年 10 月|提供支援 Windows 95 和 Windows NT Workstation 或 NT Server 3.51。 只有 32 位元驅動程式包含在此版本中。移除 Windows 3.1 版的 16 位元驅動程式。|  
|3.5|1996 年 10 月|這些驅動程式是雙位元組字元集 (DBCS)-啟用、 已比舊版中，更適合用於網際網路應用程式和容納檔案資料來源名稱 (Dsn) 的使用。 Microsoft Access 驅動程式是在 Windows 95/98 和 Windows NT 3.51 和更新版本的作業系統 Alpha 平台上使用的 RISC 版本發行。|  
|4.0|晚期 1998|提供 Microsoft Jet 引擎 Unicode 格式，以及 ANSI 格式的較早版本的相容性支援。|  
  
> [!NOTE]  
>  Version3.5 驅動程式被設計來搭配 ODBC2。*x*。 它們也會使用 ODBC 3.0，雖然它們不支援所有 ODBC 3.0 功能。 如需有關如何搭配 ODBC 3.0 這些驅動程式的運作方式的詳細資訊，請參閱[回溯相容性和標準相容性](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。
