---
description: 連線選項
title: 連接選項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection options [ODBC]
- ODBC driver for Oracle [ODBC], connection options
- custom connection options [ODBC]
ms.assetid: abfdc133-cb33-435f-a467-fbe15444f687
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 22326ca650f575c6a4f0503093306d8b68581475
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483681"
---
# <a name="connect-options"></a>連線選項
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 這些選項可讓您自訂應用程式內的資料庫連接。  
  
|Connect 選項|注意|  
|--------------------|-----------|  
|SQL_AUTOCOMMIT|如果您選擇 SQL_AUTOCOMMIT_OFF，則您的應用程式必須使用 [SQLTransact](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)明確認可或復原交易。|  
|SQL_ODBC_CURSORS|此連接屬性會在驅動程式管理員中執行。|  
|SQL_OPT_TRACE|此連接屬性會在驅動程式管理員中執行。|  
|SQL_OPT_TRACEFILE|此連接屬性會在驅動程式管理員中執行。|  
|SQL_TRANSLATE_DLL|傳回錯誤：「驅動程式無法支援」。|  
|SQL_TRANSLATE_OPTION|傳遞至轉譯 .dll 的32位值。|  
|SQL_TXN_ISOLATION|驅動程式只允許 SQL_TXN_READ_COMMITTED。<br /><br /> 不支援下列 vParams：<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
|SQL_ATTR_ENLIST_IN_DTC|如果您使用 Windows NT) ，此 ODBC 3.0 連接屬性可讓您在 Microsoft 元件服務 (或 MTS 協調的分散式交易中，使用 ODBC Driver for Oracle。 它會以*vParam*引數的形式提供*pITransaction*給交易的介面指標。|  
|SQL_ATTR_CONNECTION_DEAD|這個唯讀 ODBC 3.5 連接屬性可讓您判斷與 Oracle 伺服器的連接是否失敗。 僅限 Get;無法設定。|
