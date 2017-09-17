---
title: "可捲動資料指標和交易隔離 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 192962491095f8c6b8fb212ab7789cb74b609897
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="scrollable-cursors-and-transaction-isolation"></a>可捲動資料指標和交易隔離
下表列出控管的變更可見性的因素。  
  
|所做的變更：|可見性取決於：|  
|----------------------|----------------------------|  
|資料指標|資料指標類型，資料指標實作|  
|在相同交易中的其他陳述式|資料指標類型|  
|其他交易中的陳述式|資料指標類型，交易隔離等級|  
  
 這些因素會在下圖顯示。  
  
 ![管理變更的可見性的因素](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 下表摘要說明每個資料指標類型的偵測本身、 由其他作業在自己的交易和其他交易所變更的功能。 第二個變更的可見性取決於資料指標類型和游標所在的交易隔離等級。  
  
|資料指標 type\action|Self|擁有<br /><br /> Txn|其他<br /><br /> Txn<br /><br /> (RU[a])|其他<br /><br /> Txn<br /><br /> (RC[a])|其他<br /><br /> Txn<br /><br /> (RR[a])|其他<br /><br /> Txn<br /><br /> (S[a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|靜態|||||||  
|Insert|可能是 [b]|否|否|否|否|否|  
|Update|可能是 [b]|否|否|否|否|否|  
|DELETE|可能是 [b]|否|否|否|否|否|  
|索引鍵集導向的資料指標|||||||  
|Insert|可能是 [b]|否|否|否|否|否|  
|Update|是|是|是|是|否|否|  
|DELETE|可能是 [b]|是|是|是|否|否|  
|動態|||||||  
|Insert|是|是|是|是|是|否|  
|Update|是|是|是|是|否|否|  
|DELETE|是|是|是|是|否|否|  
  
 [a] 括號括住字元表示包含資料指標; 之交易的隔離等級（在其中變更） 的其他交易隔離等級無關。  
  
 RU-RU： 讀取未認可  
  
 RC： 讀取認可  
  
 RR： 可重複讀取  
  
 可序列化的 s:  
  
 [b] 取決於資料指標的實作方式。 資料指標是否可以偵測到這類變更會報告透過 SQL_STATIC_SENSITIVITY 選項中**SQLGetInfo**。
