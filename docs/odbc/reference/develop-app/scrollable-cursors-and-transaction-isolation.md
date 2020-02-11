---
title: 可滾動的資料指標和交易隔離 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 92e3694690ef1cba210da29766e7528762e691f2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68061605"
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>可捲動的資料指標和交易隔離
下表列出管理變更可見度的因素。  
  
|所做的變更：|可見度取決於：|  
|----------------------|----------------------------|  
|資料指標|資料指標類型，資料指標執行|  
|相同交易中的其他語句|資料指標類型|  
|其他交易中的語句|資料指標類型，交易隔離等級|  
  
 下圖顯示這些因素。  
  
 ![管理變更的可見性之因數](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 下表摘要說明每個資料指標類型用來偵測本身所做的變更、其本身的交易中的其他作業，以及其他交易的能力。 後者變更的可見度取決於資料指標類型和包含資料指標之交易的隔離等級。  
  
|資料指標 type\action|Self|各自<br /><br /> Txn|其他<br /><br /> Txn<br /><br /> （RU [a]）|其他<br /><br /> Txn<br /><br /> （RC [a]）|其他<br /><br /> Txn<br /><br /> （RR [a]）|其他<br /><br /> Txn<br /><br /> （S [a]）|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|靜態|||||||  
|插入|可能 [b]|否|否|否|否|否|  
|更新|可能 [b]|否|否|否|否|否|  
|刪除|可能 [b]|否|否|否|否|否|  
|索引鍵集導向的資料指標|||||||  
|插入|可能 [b]|否|否|否|否|否|  
|更新|是|是|是|是|否|否|  
|刪除|可能 [b]|是|是|是|否|否|  
|Dynamic|||||||  
|插入|是|是|是|是|是|否|  
|更新|是|是|是|是|否|否|  
|刪除|是|是|是|是|否|否|  
  
 [a] 以括弧括住的字母表示包含資料指標之交易的隔離等級。另一筆交易的隔離等級（已進行變更）是不相關的。  
  
 RU：讀取未認可  
  
 RC：讀取已認可  
  
 RR：可重複讀取  
  
 S： Serializable  
  
 [b] 取決於資料指標的執行方式。 資料指標是否可以透過**SQLGetInfo**中的 [SQL_STATIC_SENSITIVITY] 選項來偵測這類變更。
