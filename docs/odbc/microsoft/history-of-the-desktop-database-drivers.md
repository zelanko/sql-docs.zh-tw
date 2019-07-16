---
title: 桌面資料庫驅動程式的歷程記錄 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d225bac273558b928e3e8fd2f41bd121a723f6ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952375"
---
# <a name="history-of-the-desktop-database-drivers"></a>桌面資料庫驅動程式歷程記錄
下表顯示桌面資料庫驅動程式版本歷程記錄。  
  
|Version|發行日期|描述|  
|-------------|------------------|-----------------|  
|1.0|1993 年 8 月|使用 SIMBA 查詢處理器 PageAhead 軟體所產生。 SIMBA 收到呼叫 ODBC 和 SQL 陳述式、 Microsoft Jet 可安裝的 ISAM 呼叫，來處理它們，然後呼叫 Microsoft Jet ISAM 分派層，以載入並呼叫適當的可安裝 ISAM 驅動程式。|  
|2.0|1994 年 12 月|搭配 ODBC 2.0，可大幅擴充 ODBC 功能。 在 2.0 版中的主要變更是，Microsoft Jet 資料庫引擎已取代 SIMBA 查詢處理器。 使用 Microsoft Jet 資料庫引擎，桌面資料庫驅動程式更緊密地整合 Microsoft Jet 可安裝 ISAM 驅動程式和 Microsoft Access 技術。 已顯著的增強功能：<br /><br /> -原生支援可捲動資料指標。<br />-原生支援外部聯結、 更新和異質聯結和交易。<br />-32 位元版本的 Microsoft Windows NT 的驅動程式。|  
|3.0|1995 年 10 月|提供支援 Windows 95 和 Windows NT Workstation 或 NT 伺服器 3.51。 僅 32 位元驅動程式包含在此版本中;已移除 Windows 3.1 版的 16 位元驅動程式。|  
|3.5|1996 年 10 月|這些驅動程式是雙位元組字元集 (DBCS)-啟用、 已比舊版中，更適合用於網際網路應用程式，以及容納檔案資料來源名稱 (Dsn) 的使用。 Microsoft Access 驅動程式已發行的 Windows 95/98 和 Windows NT 3.51 和更新版本的作業系統 Alpha 平台上使用 RISC 版本。|  
|4.0|晚期 1998|提供 Microsoft Jet 引擎 Unicode 格式，以及 ANSI 格式的較早版本的相容性支援。|  
  
> [!NOTE]  
>  Version3.5 驅動程式被設計用於搭配 ODBC2。*x*。 雖然也可使用 ODBC 3.0，它們不支援所有 ODBC 3.0 功能。 如需有關這些驅動程式如何搭配 ODBC 3.0 的詳細資訊，請參閱 <<c0> [ 回溯相容性與標準相容性](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。
