---
description: 桌面資料庫驅動程式歷程記錄
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
ms.openlocfilehash: 80e8f1b52abac92ba09b97d35d45dfe0506963ec
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500321"
---
# <a name="history-of-the-desktop-database-drivers"></a>桌面資料庫驅動程式歷程記錄
下表顯示桌面資料庫驅動程式的版本歷程記錄。  
  
|版本|發行日期|描述|  
|-------------|------------------|-----------------|  
|1.0|1993年8月|使用 PageAhead Software 所產生的 SIMBA 查詢處理器。 SIMBA 收到了 ODBC 呼叫和 SQL 語句，並將其處理為 Microsoft Jet 可安裝的 ISAM 呼叫，然後呼叫 Microsoft Jet ISAM 分派層以載入及呼叫適當的可安裝的 ISAM 驅動程式。|  
|2.0|1994年12月|用於 ODBC 2.0，這是大幅擴充的 ODBC 功能。 2.0 版中的重大變更是 Microsoft Jet 資料庫引擎取代了 SIMBA 查詢處理器。 使用 Microsoft Jet database engine，桌面資料庫驅動程式與 Microsoft Jet 可安裝的 ISAM 驅動程式和 Microsoft Access 技術緊密整合，更緊密整合。 重大的增強功能如下：<br /><br /> -可滾動資料指標的原生支援。<br />-外部聯結、可更新和異類聯結以及交易的原生支援。<br />-32 位版本的適用于 Microsoft Windows NT 的驅動程式。|  
|3.0|1995年10月|提供 Windows 95 和 Windows NT 工作站或 NT Server 3.51 的支援。 此版本只包含32位驅動程式;已移除適用于 Windows 3.1 版的16位驅動程式。|  
|3.5|1996年10月|這些驅動程式是雙位元組字元集 (DBCS) 啟用，更適合與舊版網際網路應用程式搭配使用，並可 (Dsn) 使用檔案資料來源名稱。 Microsoft Access 驅動程式是以 RISC 版本發行，適用于 Windows 95/98 和 Windows NT 3.51 和更新版本作業系統的 Alpha 平臺。|  
|4.0|1998遲到|提供 Microsoft Jet Engine Unicode 格式以及舊版 ANSI 格式的相容性支援。|  
  
> [!NOTE]  
>  3.5 版驅動程式是設計來與 ODBC2 搭配使用。*x*。 雖然它們也可以搭配 ODBC 3.0 使用，但它們並不支援所有的 ODBC 3.0 功能。 如需這些驅動程式如何搭配 ODBC 3.0 運作的詳細資訊，請參閱回溯 [相容性和標準合規性](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。
