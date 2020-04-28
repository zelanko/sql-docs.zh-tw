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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8e5f15575d34031d9886219af5677b4fc5f1d5aa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301531"
---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption (Access 驅動程式)
> [!NOTE]  
>  本主題提供存取驅動程式特定的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
|fOption|註解|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption 可以設定為 SQL_MODE_READ_ONLY 或 SQL_MODE_READ_WRITE。 不過，如果 SQL_ACCESS_MODE 設定為 SQL_MODE_READ_ONLY，驅動程式不會阻止更新。|  
|SQL_AUTOCOMMIT|使用 Microsoft Access 驅動程式時，[SQL_AUTOCOMMIT] 選項可能會設定為 [SQL_AUTOCOMMIT_ON] 或 [SQL_AUTOCOMMIT_OFF]，因為 Microsoft Access 驅動程式支援交易 [1]。|  
|SQL_CURRENT_QUALIFIER|支援。|  
|SQL_LOGIN_TIMEOUT|不支援。|  
|SQL_OPT_TRACE|支援。|  
|SQL_OPT_TRACEFILE|支援。|  
|SQL_PACKET_SIZE|不支援。|  
|SQL_QUIET_MODE|不支援。|  
|SQL_TRANSLATE_DLL|不支援。|  
|SQL_TRANSLATION_OPTION|不支援。|  
|SQL_TXN_ISOLATION|一律會 SQL_TXN_READ_COMMITTED SQL_TXN_ISOLATION。|  
  
 [1] Microsoft Access 驅動程式不支援不可部分完成的交易。 使用 Microsoft Access 驅動程式來認可交易時，在認可交易的時間和將值寫入磁片的時間之間會有有限的延遲。 此延遲取決於 Microsoft Jet 引擎中的固有延遲。 頁面超時不會小於最小值，即使 PageTimeout 選項設定為低於該值也一樣。 因此，不保證認可的資料會穩定，因為可能會在延遲期間進行變更。
