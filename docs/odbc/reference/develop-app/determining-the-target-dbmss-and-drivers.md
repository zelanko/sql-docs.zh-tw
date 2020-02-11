---
title: 判斷目標 Dbms 和驅動程式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7065aa88d60a508df9946d38d0dded220c4bb7a1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68106146"
---
# <a name="determining-the-target-dbmss-and-drivers"></a>判斷目標 DBMS 和驅動程式
下一個要考慮的問題是，應用程式的目標 Dbms 為何，以及支援這些 Dbms 的驅動程式有哪些？ 因為泛型應用程式通常是高度互通，所以目標 Dbms 的問題最適用于自訂和垂直應用程式。 不過，目標驅動程式的問題適用于所有應用程式，因為驅動程式的速度、品質、功能支援和可用性各有很大的差異。 此外，如果要隨著應用程式轉散發驅動程式，則需要考慮授權方案的成本和可用性。  
  
 對於許多自訂應用程式而言，目標 Dbms 很明顯：這些是應用程式設計來存取的現有 Dbms。 也應該考慮未來要進行遷移的 Dbms。 不過，這些應用程式的主要問題是與它們搭配使用的驅動程式或驅動程式。 針對其他自訂應用程式（其並非設計用來存取現有的 DBMS），可以根據功能支援、並行使用者支援、驅動程式可用性和實惠來選擇目標 Dbms。  
  
 針對垂直應用程式，通常會根據功能支援、驅動程式可用性和市場來選擇目標 Dbms。 例如，針對小型企業所設計的垂直應用程式，必須以 Dbms 為目標，這些企業可為他們提供實惠;設計為現有 Dbms 之附加元件的垂直應用程式必須以廣泛使用的 Dbms 為目標。  
  
 選擇目標 Dbms 時，應該考慮桌上型電腦與伺服器資料庫之間的差異。 桌面資料庫（例如 dBASE、Paradox 和 Btrieve）的功能比伺服器資料庫低。 因為它們通常是透過大部分以檔案為基礎之驅動程式中較不強大的 SQL 引擎來存取，所以它們通常缺乏完整的交易支援、支援較少的並行使用者，而且具有有限的 SQL。 不過，它們的價格低廉，而且有一個大型安裝的基底。  
  
 Oracle、DB2 和 SQL Server 等伺服器資料庫提供完整的交易支援、支援許多並行使用者，而且具有豐富的 SQL。 它們的成本更高，而且已安裝較小的基底。 相反地，軟體價格通常會較高，有些則會抵消較小的潛在市場。  
  
 因此，有時可以根據應用程式和應用程式的目標市場所需的功能來選擇目標 Dbms。 例如，大型企業的訂單輸入系統可能不會以桌面資料庫為目標，因為這類交易支援不足。 針對小型企業所設計的類似系統，可能會以成本為單位排除大部分的伺服器資料庫。 和一般應用程式的開發人員可能會以兩者為目標，但避免使用在伺服器資料庫中找到的 advanced 功能。
