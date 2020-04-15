---
title: 確定目標 DBMS 和驅動程式 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- target DBMSs and drivers in interoperability [ODBC]
- interoperability [ODBC], target dbmss and drivers
ms.assetid: 23bee0f6-e12a-4598-b34e-df11a8086829
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f8811e4d289a8fc89c2c3773aab973df523025f5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305869"
---
# <a name="determining-the-target-dbmss-and-drivers"></a>判斷目標 DBMS 和驅動程式
需要考慮的下一個問題是,應用程式的目標 DBMS 是什麼,哪些驅動程式支援這些 DBMS? 由於通用應用程式往往高度可互通,因此目標 DBMS 問題最適用於自訂和垂直應用程式。 但是,目標驅動程式的問題適用於所有應用程式,因為驅動程式在速度、品質、功能支援和可用性方面差異很大。 此外,如果要與應用程式重新分發驅動程式,需要考慮許可計劃的成本和可用性。  
  
 對於許多自定義應用程式,目標 DBMS 是顯而易見的:它們是應用程式設計為要訪問的現有 DBMS。 還應考慮計劃向其遷移的 DBMS。 但是,對於這些應用程序來說,主要問題是要使用它們的驅動程式或驅動程式。 對於其他自定義應用程式(那些不是旨在存取現有 DBMS 的應用程式),可以根據功能支援、併發使用者支援、驅動程式可用性和可負擔性選擇目標 DBMS。  
  
 對於垂直應用,目標DBMS通常基於功能支援、驅動程式可用性和市場進行選擇。 例如,專為小型企業設計的垂直應用程序必須針對這些企業負擔得起的 DBMS;設計為現有 DBMS 的附加元件的垂直應用程式必須針對廣泛使用的 DBMS。  
  
 在選擇目標 DBMS 時,應考慮桌面資料庫和伺服器資料庫之間的差異。 桌面資料庫(如 dBASE、Paradox 和 Btrieve)不如伺服器資料庫強大。 因為它們通常通過大多數基於檔的驅動程式中功能較弱的 SQL 引擎進行訪問,因此它們通常缺乏完整的事務支援,支援較少的併發使用者,並且 SQL 有限。 但是,它們價格低廉,並且具有較大的客戶群。  
  
 Oracle、DB2 和 SQL Server 等伺服器資料庫提供完整的事務支援、支援許多併發使用者以及具有豐富的 SQL。 它們的成本要高得多,而且安裝基礎更小。 另一方面,軟體價格往往較高,多少抵消了較小的潛在市場。  
  
 因此,有時可以根據應用程式和應用程式的目標市場所需的功能選擇目標 DBMS。 例如,大型企業的訂單輸入系統可能不是針對桌面資料庫的目標,因為這些資料庫缺乏足夠的事務支援。 為小型企業設計的類似系統可能會根據成本排除大多數伺服器資料庫。 通用應用程式的開發人員可能同時針對這兩種功能,但應避免使用伺服器資料庫中的高級功能。
