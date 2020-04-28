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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89434b397c07fdee751ca4272b65ac2eada94cf3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304979"
---
# <a name="history-of-the-desktop-database-drivers"></a>桌面資料庫驅動程式歷程記錄
下表顯示桌面資料庫驅動程式版本歷程記錄。  
  
|版本|發行日期|描述|  
|-------------|------------------|-----------------|  
|1.0|1993年8月|使用 PageAhead 軟體所產生的 SIMBA 查詢處理器。 SIMBA 收到了 ODBC 呼叫和 SQL 語句，將它們處理成 Microsoft Jet 可安裝的 ISAM 呼叫，然後呼叫 Microsoft Jet ISAM 分派層來載入和呼叫適當的可安裝的 ISAM 驅動程式。|  
|2.0|1994年12月|與 ODBC 2.0 搭配使用，這會大幅擴充 ODBC 功能。 2.0 版的主要變更是 Microsoft Jet 資料庫引擎已取代 SIMBA 查詢處理器。 透過 Microsoft Jet 資料庫引擎，桌面資料庫驅動程式整合了更緊密的 Microsoft Jet 可安裝的 ISAM 驅動程式和 Microsoft Access 技術。 重大的增強功能：<br /><br /> -可滾動資料指標的原生支援。<br />-外部聯結、可更新和異類聯結，以及交易的原生支援。<br />-32-位版本的 Microsoft Windows NT 驅動程式。|  
|3.0|1995年10月|提供 Windows 95 和 Windows NT 工作站或 NT Server 3.51 的支援。 此版本僅包含32位驅動程式;已移除 Windows 3.1 版的16位驅動程式。|  
|3.5|1996年10月|這些驅動程式已啟用雙位元組字元集（DBCS），更適合與舊版的網際網路應用程式搭配使用，並配合檔案資料來源名稱（Dsn）的使用。 Microsoft Access 驅動程式已在 RISC 版本中發行，以用於 Windows 95/98 和 Windows NT 3.51 及更新版本作業系統的 Alpha 平臺。|  
|4.0|1998晚期|提供 Microsoft Jet 引擎 Unicode 格式的支援，以及舊版的 ANSI 格式相容性。|  
  
> [!NOTE]  
>  3.5 版驅動程式的設計目的是要與 ODBC2 搭配使用。*x*。 雖然它們也可以與 ODBC 3.0 搭配使用，但它們並不支援所有的 ODBC 3.0 功能。 如需這些驅動程式如何與 ODBC 3.0 搭配使用的詳細資訊，請參閱回溯[相容性和標準合規性](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。
