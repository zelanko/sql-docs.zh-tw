---
description: 判斷目標 DBMS 和驅動程式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8dfbc11e96577e9027d1cc6e17701a82b89061be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429320"
---
# <a name="determining-the-target-dbmss-and-drivers"></a>判斷目標 DBMS 和驅動程式
下一個要考慮的問題是，應用程式的目標 Dbms 有哪些，以及哪些驅動程式可支援這些 Dbms？ 因為一般應用程式通常會有高度互通，所以目標 Dbms 的問題最適用于自訂和垂直應用程式。 不過，目標驅動程式的問題會套用至所有應用程式，因為驅動程式的速度、品質、功能支援和可用性會有很大的差異。 此外，如果要與應用程式一起轉散發驅動程式，則必須考慮授權方案的成本和可用性。  
  
 在許多自訂應用程式中，目標 Dbms 很明顯：它們是應用程式設計來存取的現有 Dbms。 您也應該考慮未來要進行遷移的 Dbms。 不過，這些應用程式的主要問題是要搭配它們使用的驅動程式或驅動程式。 針對其他自訂應用程式（不是設計用來存取現有 DBMS 的應用程式），可以根據功能支援、並行使用者支援、驅動程式可用性和可負擔性來選擇目標 Dbms。  
  
 若是垂直應用程式，通常會根據功能支援、驅動程式可用性和市場來選擇目標 Dbms。 例如，專為小型企業設計的垂直應用程式，必須以這些企業實惠的 Dbms 為目標。設計為現有 Dbms 附加元件的垂直應用程式必須以廣泛使用的 Dbms 為目標。  
  
 選擇目標 Dbms 時，應考慮桌上型電腦和伺服器資料庫之間的差異。 Desktop 資料庫（例如 dBASE、Paradox 和 Btrieve）比伺服器資料庫的功能強大。 因為它們通常是透過大多數以檔案為基礎之驅動程式中較不強大的 SQL 引擎來存取，所以它們通常不會有完整的交易支援、支援較少的並行使用者，並擁有有限的 SQL。 不過，它們的價格較低，而且會有一個大型安裝的基底。  
  
 伺服器資料庫（例如 Oracle、DB2 和 SQL Server）提供完整的交易支援、支援許多並行使用者，而且擁有豐富的 SQL。 它們的成本較高，且安裝的基礎較小。 另一方面，軟體價格通常會更高，而稍微偏移較小的潛在市場。  
  
 因此，有時可以根據應用程式和應用程式目標市場所需的功能來選擇目標 Dbms。 例如，大型公司的訂單輸入系統可能不會以桌面資料庫為目標，因為這些都沒有足夠的交易支援。 專為小型企業設計的類似系統可能會以成本為基礎排除大部分的伺服器資料庫。 和一般應用程式的開發人員可能會以兩者為目標，但會避免使用在伺服器資料庫中找到的 advanced 功能。
