---
title: SQLSet連接選項(dBASE 驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], dBASE Driver
ms.assetid: b1924c33-6820-4566-b716-6897807edd0f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 32bfb4755d308706372c0d863f8246631c122f21
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301519"
---
# <a name="sqlsetconnectoption-dbase-driver"></a>SQLSetConnectOption (dBASE 驅動程式)
> [!NOTE]  
>  本主題提供特定於 dBASE 驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
|fOption|註解|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption 可以設置為SQL_MODE_READ_ONLY或SQL_MODE_READ_WRITE。 但是,如果SQL_ACCESS_MODE設置為SQL_MODE_READ_ONLY,則驅動程式不會阻止更新。|  
|SQL_AUTOCOMMIT|dBASE 驅動程式僅支援SQL_AUTOCOMMIT設定為 ON(預設狀態),因為它不支援事務。|  
|SQL_CURRENT_QUALIFIER|支援。|  
|SQL_LOGIN_TIMEOUT|不支援。|  
|SQL_OPT_TRACE|支援。|  
|SQL_OPT_TRACEFILE|支援。|  
|SQL_PACKET_SIZE|不支援。|  
|SQL_QUIET_MODE|不支援。|  
|SQL_TRANSLATE_DLL|不支援。|  
|SQL_TRANSLATION_OPTION|不支援。|  
|SQL_TXN_ISOLATION|不支援。|
