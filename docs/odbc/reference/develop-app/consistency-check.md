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
ms.openlocfilehash: 419e338a5e96821606dc26a53a4fccecbc72ae3e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125531"
---
# <a name="consistency-check"></a>一致性檢查
每當應用程式設定 APD、ARD 或 IPD 的 SQL_DESC_DATA_PTR 欄位時，驅動程式就會自動執行一致性檢查。 每當設定此欄位時，驅動程式會檢查 [SQL_DESC_TYPE] 欄位的值，以及適用于相同記錄中 [SQL_DESC_TYPE] 欄位的值是否有效且一致。  
  
 IPD 的 SQL_DESC_DATA_PTR 欄位通常不會設定;不過，應用程式可以這樣做，以強制執行 IPD 欄位的一致性檢查。 IPD 的 SQL_DESC_DATA_PTR 欄位設定為的值實際上並不會儲存，而且無法藉由呼叫**SQLGetDescField**或**SQLGetDescRec**來抓取;此設定只會用來強制執行一致性檢查。 無法在 IRD 上執行一致性檢查。  
  
 如需一致性檢查的詳細資訊，請參閱[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。
