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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106146"
---
# <a name="determining-the-target-dbmss-and-drivers"></a>判斷目標 DBMS 和驅動程式
考慮下一個問題是，什麼是應用程式的目標 Dbms 哪些驅動程式是否可用，以及支援這些 Dbms？ 一般應用程式通常為高度互通，因為目標 Dbms 的問題是最適用於自訂和垂直應用程式。 不過，目標驅動程式問題適用於所有應用程式，因為驅動程式所帶來的速度、 品質、 功能的支援，和可用性。 此外，如果驅動程式與應用程式轉散發，成本和可用性的授權計劃需要考量。  
  
 許多自訂應用程式，目標 Dbms 都很明顯：他們現有的 Dbms 應用程式是設計用來存取。 也應該考慮的 Dbms 的規劃未來的移轉。 不過，這些應用程式的主要問題是哪一個驅動程式或驅動程式，以使用它們。 其他自訂的應用程式-那些並非設計來存取現有的 DBMS-目標 Dbms 可選擇根據所支援之功能、 並行使用者支援、 驅動程式的可用性，以及選擇。  
  
 對於垂直的應用程式，通常會選擇 Dbms 的目標會根據所支援之功能、 驅動程式的可用性和市場。 例如，適用於小型企業設計的垂直應用程式必須為目標是這類企業; 價格合理的 Dbms垂直的應用程式，設計成可附加至現有的 Dbms 元件必須為目標，廣泛用於 Dbms。  
  
 選擇目標 Dbms 時, 應該考量桌面和伺服器的資料庫之間的差異。 DBASE、 Paradox，等 Btrieve 桌面資料庫是較不強大比伺服器資料庫。 它們通常透過較不強大的 SQL 引擎找到最以檔案為基礎的驅動程式中存取，因此它們通常缺乏完整的交易支援、 支援較少的並行使用者，且具有有限的 SQL。 不過，它們便宜，而且有一個大型安裝基底。  
  
 伺服器的資料庫，例如 Oracle、 DB2 與 SQL Server 提供完整的交易支援，支援許多並行使用者，並具有豐富的 SQL。 它們更為昂貴，而且有一個較小安裝基底。 相反地，軟體價格通常會更高、 有點位移較小的潛在市場。  
  
 因此，您可以有時目標 Dbms 選擇為根據的應用程式和應用程式的目標市場所需的功能。 例如，訂單輸入系統為大型公司不可能目標桌面資料庫，因為這些缺少適當的交易支援。 適用於小型企業而設計的類似系統可能會排除大部分以成本為基礎的伺服器資料庫。 和一般應用程式的開發人員可能會同時為目標，但最好避免使用伺服器資料庫中的進階的功能。
