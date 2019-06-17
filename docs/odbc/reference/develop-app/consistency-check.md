---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cb73d8a4de482f24eae5794232019af9890e3624
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63043733"
---
# <a name="consistency-check"></a>一致性檢查
一致性檢查會驅動程式自動執行應用程式在設定 SQL_DESC_DATA_PTR 欄位 APD、 ARD，或 IPD 時。 每當設定此欄位時，驅動程式會檢查的 SQL_DESC_TYPE 欄位的值，而且適用於同一筆記錄中的 SQL_DESC_TYPE 欄位的值有效且一致。  
  
 通常未設定 SQL_DESC_DATA_PTR 欄位的 IPD;不過，應用程式可以先註冊才能強制執行一致性檢查的 IPD 欄位。 IPD 的 SQL_DESC_DATA_PTR 欄位設定為值並非實際儲存，而且無法擷取由呼叫**SQLGetDescField**或是**SQLGetDescRec**; 此設定只對強制一致性檢查。 無法在 IRD 上執行一致性檢查。  
  
 如需有關一致性檢查的詳細資訊，請參閱 < [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。
