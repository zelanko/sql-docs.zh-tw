---
title: 判斷目標 Dbms 和驅動程式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- target DBMSs and drivers in interoperability [ODBC]
- interoperability [ODBC], target dbmss and drivers
ms.assetid: 23bee0f6-e12a-4598-b34e-df11a8086829
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fd4dc48994a028b2f8569da05511fa5c2b078165
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="determining-the-target-dbmss-and-drivers"></a>判斷目標 Dbms 和驅動程式
考慮下一個問題是，為何，應用程式的目標 Dbms 哪些驅動程式是否可用，以及支援那些 Dbms？ 泛型應用程式通常是具備高度互通性，因為目標 Dbms 的問題，最適合用於自訂和垂直應用程式使用。 不過，目標驅動程式的問題適用於所有應用程式，因為驅動程式相當廣泛的速度、 品質、 功能支援和可用性。 此外，如果驅動程式與應用程式轉散發，則成本和可用性的授權計劃需要考量。  
  
 對於許多的自訂應用程式，目標 Dbms 會明顯： 現有 Dbms 應用程式是設計用來存取。 也應該考量未來移轉為計劃的 Dbms。 不過，這些應用程式的主要問題是它們搭配使用的驅動程式。 其他自訂應用程式 — 的設計並不適用於存取現有的 DBMS — 可以根據功能的支援、 並行使用者支援、 驅動程式的可用性和負擔選擇目標 Dbms。  
  
 對於垂直的應用程式，通常會選擇 Dbms 目標會根據功能的支援、 驅動程式的可用性和市場。 例如，適用於小型企業所設計的垂直應用程式必須為目標是這些商務; 價格合理的 Dbms設計作為目標的現有 Dbms 附加元件必須廣泛的垂直應用程式使用 Dbms。  
  
 選擇目標 Dbms 時，應該考量桌上型電腦和伺服器的資料庫之間的差異。 例如 dBASE、 Paradox 和 Btrieve 桌面資料庫是較不強大比伺服器資料庫。 因為它們通常透過較不強大的 SQL 引擎找到最以檔案為基礎的驅動程式中存取，它們通常缺少完整交易的支援、 支援較少的並行使用者，且具有有限的 SQL。 不過，它們便宜，而且有大型的已安裝基底。  
  
 伺服器的資料庫，例如 Oracle、 DB2 和 SQL Server 提供完整的交易支援，支援許多並行使用者，而且包含豐富的 SQL。 它們更為昂貴，而且有較小的大小已安裝基底。 相反地，軟體價格通常會比較高，有些位移較小的潛在市場。  
  
 因此，您可以目標有時 Dbms 選為根據的應用程式和應用程式的目標市場所需的功能。 例如，訂單輸入系統的大型企業可能不目標桌面資料庫因為這些缺少足夠的交易支援。 適用於小型企業所設計的類似系統可能會排除大部分的伺服器資料庫，以成本為基礎。 與泛型應用程式的開發人員可能會同時為目標，但請避免使用伺服器資料庫中的進階的功能。
