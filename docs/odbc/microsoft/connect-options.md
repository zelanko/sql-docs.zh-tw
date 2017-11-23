---
title: "連接選項 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection options [ODBC]
- ODBC driver for Oracle [ODBC], connection options
- custom connection options [ODBC]
ms.assetid: abfdc133-cb33-435f-a467-fbe15444f687
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 43cb42e7d77cbf3471f2475af5290ba045db05fa
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="connect-options"></a>連接選項
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 這些選項可讓自訂的應用程式中的資料庫連接。  
  
|連接選項|注意|  
|--------------------|-----------|  
|SQL_AUTOCOMMIT|如果您選擇 SQL_AUTOCOMMIT_OFF 時，您的應用程式必須明確地認可或回復與交易[SQLTransact](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)。|  
|SQL_ODBC_CURSORS|此連接屬性會實作驅動程式管理員。|  
|SQL_OPT_TRACE|此連接屬性會實作驅動程式管理員。|  
|SQL_OPT_TRACEFILE|此連接屬性會實作驅動程式管理員。|  
|SQL_TRANSLATE_DLL|會傳回錯誤: 「 驅動程式不支援。 」|  
|SQL_TRANSLATE_OPTION|32 位元值傳遞給轉譯.dll。|  
|SQL_TXN_ISOLATION|驅動程式可讓您僅 SQL_TXN_READ_COMMITTED。<br /><br /> 不支援下列 vParams:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE 的情況下|  
|SQL_ATTR_ENLIST_IN_DTC|此 ODBC 3.0 連接屬性可讓您使用 oracle 的 ODBC 驅動程式由 Microsoft 元件服務 （或 MTS，如果您使用 Windows NT） 協調的分散式交易中。 它提供的介面指標*pITransaction*做為交易*vParam*引數。|  
|SQL_ATTR_CONNECTION_DEAD|此唯讀 ODBC 3.5 連接屬性可讓您判斷是否有失敗 Oracle 伺服器的連線。 取得; 僅限無法設定。|
