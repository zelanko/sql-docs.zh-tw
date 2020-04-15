---
title: 一致性檢查 |微軟文件
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
ms.openlocfilehash: edd946ca865cd9d8d2edff2c7bedbb3b2629c97c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298998"
---
# <a name="consistency-check"></a>一致性檢查
每當應用程式設定 APD、ARD 或 IPD 的SQL_DESC_DATA_PTR欄位時,驅動程式會自動執行一致性檢查。 每當設定此欄位時,驅動程式都會檢查SQL_DESC_TYPE欄位的值和適用於同一記錄中SQL_DESC_TYPE欄位的值是否有效且一致。  
  
 通常不設置 IPD 的SQL_DESC_DATA_PTR欄位;但是,應用程式可以這樣做來強制對 IPD 欄位進行一致性檢查。 IPD 的SQL_DESC_DATA_PTR欄位的值實際上未儲存,並且無法透過呼叫**SQLGetDescField**或**SQLGetDescRec**檢索該值。設置僅用於強制一致性檢查。 無法對 IRD 執行一致性檢查。  
  
 有關一致性檢查的詳細資訊,請參閱[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。
