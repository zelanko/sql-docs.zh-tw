---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 06695bf1770c9e362decac5702dcd924d47c23bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63301766"
---
# <a name="connect-options"></a>連線選項
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用所提供的 ODBC 驅動程式。  
  
 這些選項可讓自訂應用程式內的資料庫連接。  
  
|連線選項|注意|  
|--------------------|-----------|  
|SQL_AUTOCOMMIT|如果您選擇 SQL_AUTOCOMMIT_OFF 時，您的應用程式必須明確地認可或回復交易[SQLTransact](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)。|  
|SQL_ODBC_CURSORS|此連接屬性會實作驅動程式管理員。|  
|SQL_OPT_TRACE|此連接屬性會實作驅動程式管理員。|  
|SQL_OPT_TRACEFILE|此連接屬性會實作驅動程式管理員。|  
|SQL_TRANSLATE_DLL|會傳回錯誤：「 驅動程式不支援。 」|  
|SQL_TRANSLATE_OPTION|32 位元值傳遞至轉譯.dll。|  
|SQL_TXN_ISOLATION|驅動程式可讓只 SQL_TXN_READ_COMMITTED。<br /><br /> 不支援下列 vParams:<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
|SQL_ATTR_ENLIST_IN_DTC|此 ODBC 3.0 連接屬性，可讓您在 Microsoft 元件服務 （或 MTS，如果您使用 Windows NT） 所協調的分散式交易中，使用適用於 Oracle 的 ODBC 驅動程式。 它提供的介面指標*pITransaction*做為交易*vParam*引數。|  
|SQL_ATTR_CONNECTION_DEAD|此唯讀 ODBC 3.5 連接屬性可讓您判斷是否有失敗的連接到 Oracle 伺服器。 僅; get無法設定。|
