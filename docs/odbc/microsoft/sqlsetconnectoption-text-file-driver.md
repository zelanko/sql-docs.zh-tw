---
description: SQLSetConnectOption (文字檔驅動程式)
title: SQLSetConnectOption (文字檔驅動程式) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Text File Driver
- text file driver [ODBC], SQLSetConnectOption
ms.assetid: b631a20c-2f60-4102-a61d-93b8780a4620
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2247c6692da4ad88a51a69107f5f104df95eb96f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411624"
---
# <a name="sqlsetconnectoption-text-file-driver"></a>SQLSetConnectOption (文字檔驅動程式)
> [!NOTE]  
>  本主題提供文字檔驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
|fOption|註解|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption 可以設定為 SQL_MODE_READ_ONLY 或 SQL_MODE_READ_WRITE。 但是，如果 SQL_ACCESS_MODE 設定為 SQL_MODE_READ_ONLY，驅動程式不會防止更新。|  
|SQL_AUTOCOMMIT|Text 驅動程式只支援將 SQL_AUTOCOMMIT 設定為 ON (預設狀態) ，因為它們不支援交易。|  
|SQL_CURRENT_QUALIFIER|支援。|  
|SQL_LOGIN_TIMEOUT|不支援。|  
|SQL_OPT_TRACE|支援。|  
|SQL_OPT_TRACEFILE|支援。|  
|SQL_PACKET_SIZE|不支援。|  
|SQL_QUIET_MODE|不支援。|  
|SQL_TRANSLATE_DLL|不支援。|  
|SQL_TRANSLATION_OPTION|不支援。|  
|SQL_TXN_ISOLATION|不支援。|
