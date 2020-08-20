---
description: 並行類型
title: 並行類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- locking concurrency control [ODBC]
- optimistic concurrency [ODBC]
- read-only concurrency control [ODBC]
ms.assetid: 46762ae5-17dd-4777-968e-58156f470fe1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d55740b71d4e9a7d3b8d22400da0c5b3d94e73d3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461540"
---
# <a name="concurrency-types"></a>並行類型
為了解決資料指標中減少並行的問題，ODBC 公開四種不同類型的資料指標平行存取：  
  
-   **唯讀** 資料指標可以讀取資料，但無法更新或刪除資料。 這是預設的並行類型。 雖然 DBMS 可能會鎖定資料列以強制執行可重複讀取和可序列化的隔離等級，但它可以使用讀取鎖定而不是寫入鎖定。 這會導致較高的平行存取，因為其他交易至少可以讀取資料。  
  
-   **鎖定** 資料指標會使用所需的最低鎖定層級，以確保它可以更新或刪除結果集中的資料列。 這通常會導致極低的並行層級，特別是在可重複讀取和可序列化的交易隔離等級。  
  
-   使用**資料列版本的開放式平行存取和使用值的開放式並行**存取資料指標使用開放式平行存取：只有在上次讀取資料列之後，才會更新或刪除資料列。 為了偵測變更，它會比較資料列版本或值。 資料指標將無法更新或刪除資料列，但是並行處理的速度遠高於使用鎖定的時間。 如需詳細資訊，請參閱下一節： [開放式並行](../../../odbc/reference/develop-app/optimistic-concurrency.md)存取。  
  
 應用程式會指定要將資料指標與 SQL_ATTR_CONCURRENCY 語句屬性搭配使用的並行類型。 為了判斷支援的類型，它會使用 SQL_SCROLL_CONCURRENCY 選項來呼叫 **SQLGetInfo** 。
