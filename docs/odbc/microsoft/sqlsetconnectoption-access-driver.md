---
title: SQLSetConnectOption （Access 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], Access Driver
ms.assetid: 58399bc4-d0b1-4eaa-a474-c92b2d5855ea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 18950d49afdab8517b95c59df8841c33b5d3d086
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305636"
---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption (Access 驅動程式)
> [!NOTE]  
>  本主題提供存取驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|fOption|註解|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption 可以設 SQL_MODE_READ_ONLY 或 SQL_MODE_READ_WRITE。 不過，此驅動程式無法防止更新，如果 SQL_ACCESS_MODE 設 SQL_MODE_READ_ONLY。|  
|SQL_AUTOCOMMIT|使用 Microsoft Access 驅動程式時，SQL_AUTOCOMMIT 選項可能會設定為 SQL_AUTOCOMMIT_ON 或 SQL_AUTOCOMMIT_OFF，因為 Microsoft Access 驅動程式支援交易 [1]。|  
|SQL_CURRENT_QUALIFIER|支援。|  
|SQL_LOGIN_TIMEOUT|不支援。|  
|SQL_OPT_TRACE|支援。|  
|SQL_OPT_TRACEFILE|支援。|  
|SQL_PACKET_SIZE|不支援。|  
|SQL_QUIET_MODE|不支援。|  
|SQL_TRANSLATE_DLL|不支援。|  
|SQL_TRANSLATION_OPTION|不支援。|  
|SQL_TXN_ISOLATION|SQL_TXN_ISOLATION 總是 SQL_TXN_READ_COMMITTED。|  
  
 [Microsoft Access 驅動程式不支援 1] 不可部分完成交易。 認可時使用 Microsoft Access 驅動程式的交易，會認可交易的時間之間的值會寫入的時間是否存在有限的延遲到磁碟。 此延遲取決於 Microsoft Jet 引擎中固有的延遲。 在頁面上的逾時不會小於最小的值，即使 PageTimeout 選項設定的值如下。 如此一來，有已認可的資料不保證有穩定，因為可能會變更延遲期間。
