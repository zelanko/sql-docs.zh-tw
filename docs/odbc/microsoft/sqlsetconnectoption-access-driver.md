---
title: SQLSetConnectOption （存取驅動程式） |Microsoft 文件
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
- Access driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], Access Driver
ms.assetid: 58399bc4-d0b1-4eaa-a474-c92b2d5855ea
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 952bfe683dabbcedeb771c0e7f1787f7a0e6f7bb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32905013"
---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption （存取驅動程式）
> [!NOTE]  
>  本主題提供存取驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|fOption|註解|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption 可以設 SQL_MODE_READ_ONLY 或 SQL_MODE_READ_WRITE。 不過，驅動程式不會防止更新如果 SQL_ACCESS_MODE 設 SQL_MODE_READ_ONLY。|  
|SQL_AUTOCOMMIT|使用 Microsoft Access 驅動程式時，SQL_AUTOCOMMIT 選項可能會設定為 SQL_AUTOCOMMIT_ON 或 SQL_AUTOCOMMIT_OFF，因為 Microsoft Access 驅動程式支援交易 [1]。|  
|SQL_CURRENT_QUALIFIER|支援。|  
|SQL_LOGIN_TIMEOUT|不支援。|  
|SQL_OPT_TRACE|支援。|  
|SQL_OPT_TRACEFILE|支援。|  
|SQL_PACKET_SIZE|不支援。|  
|SQL_QUIET_MODE|不支援。|  
|SQL_TRANSLATE_DLL|不支援。|  
|SQL_TRANSLATION_OPTION|不支援。|  
|SQL_TXN_ISOLATION|SQL_TXN_ISOLATION 永遠是 SQL_TXN_READ_COMMITTED。|  
  
 [1] 不可部分完成交易不會受到 Microsoft Access 驅動程式。 認可交易，使用 Microsoft Access 驅動程式，有限的延遲會存在就會認可交易的時間之間的時間，此值會寫入至磁碟。 此延遲取決於 Microsoft Jet 引擎中固有的延遲。 頁面逾時不會小於最小值，即使 PageTimeout 選項設定低於的值。 如此一來，沒有認可的資料不保證很穩定，因為可能會變更延遲期間。
