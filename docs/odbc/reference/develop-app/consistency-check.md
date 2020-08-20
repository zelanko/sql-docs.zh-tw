---
description: 一致性檢查
title: 一致性檢查 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], consistency checks
- consistency checks [ODBC]
ms.assetid: deb80efa-ad1f-4ea5-b334-9817cd279e5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ad1ffe0cb7819447a3819d73cd6605347b756ede
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465900"
---
# <a name="consistency-check"></a>一致性檢查
當應用程式設定 APD、ARD 或 IPD 的 SQL_DESC_DATA_PTR 欄位時，驅動程式會自動執行一致性檢查。 每次設定此欄位時，驅動程式都會檢查 [SQL_DESC_TYPE] 欄位的值，以及在相同記錄中適用于 SQL_DESC_TYPE 欄位的值是否有效且一致。  
  
 IPD 的 SQL_DESC_DATA_PTR 欄位通常不會設定;不過，應用程式可以這樣做，以強制執行 IPD 欄位的一致性檢查。 **SQLGetDescField**或**SQLGetDescRec**的呼叫不會實際儲存 IPD 的 SQL_DESC_DATA_PTR 欄位，而且無法透過呼叫來抓取此值;這項設定只會強制執行一致性檢查。 無法在 IRD 上執行一致性檢查。  
  
 如需一致性檢查的詳細資訊，請參閱 [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。
