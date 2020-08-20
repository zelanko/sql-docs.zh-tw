---
description: 狀態記錄的順序
title: 狀態記錄的順序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 0e0436cc-230f-44b0-b373-04a57e83ee76
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2cb519cab987a1abd924f1b779a7f07c3201475
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476450"
---
# <a name="sequence-of-status-records"></a>狀態記錄的順序
如果傳回兩個以上的狀態記錄，驅動程式管理員和驅動程式會根據下列規則將其排名。 具有最高排名的記錄是第一筆記錄。 排名記錄時，不會考慮記錄 (驅動程式管理員、驅動程式、閘道等) 的來源。  
  
-   **錯誤** 描述錯誤的狀態記錄具有最高等級。 在錯誤記錄中，表示交易失敗或可能交易失敗的記錄 outrank 所有其他記錄。 如果有兩個以上的記錄描述相同的錯誤狀況，SQLSTATEs) outrank ODBC 定義和驅動程式定義 SQLSTATEs 的 Open Group CLI (規格所定義的。  
  
-   **執行-未定義資料值** 描述驅動程式未定義任何資料值 (類別 02) 具有第二個最高排名的狀態記錄。  
  
-   **警告** 描述 (類別 01) 之警告的狀態記錄具有最低等級。 如果有兩個以上的記錄描述相同的警告條件，則會 outrank ODBC 定義和驅動程式定義的 SQLSTATEs 所定義的警告 SQLSTATEs。  
  
 如果有兩個以上具有最高排名的記錄，則不會定義哪一個記錄是第一筆記錄。 所有其他記錄的順序未定義。 尤其是，由於警告可能會在錯誤之前出現，因此當函式傳回 SQL_SUCCESS 以外的值時，應用程式應該檢查所有狀態記錄。
