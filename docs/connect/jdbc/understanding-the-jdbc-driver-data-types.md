---
title: 了解 JDBC Driver 資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7802328d-4d23-4775-9573-4169b127d258
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e74573c676cb7793beff55dc478e79c7f4c5bdd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47730506"
---
# <a name="understanding-the-jdbc-driver-data-types"></a>了解 JDBC Driver 資料類型

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支援在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當作其資料庫的 Java 應用程式中，使用 JDBC 基本和進階資料類型。  
  
JDBC 類型系統會調解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型和 Java 語言類型與物件之間的轉換。 JDBC 類型的模型是以 SQL-92 和 SQL-99 類型建立的。 JDBC 驅動程式遵守 JDBC 規格，其設計在於提供可預測性與彈性之間的正確平衡。  
  
本節中的主題描述如何使用基本和進階資料類型，以及如何將資料類型轉換為其他資料類型。  
  
## <a name="in-this-section"></a>本節內容  
  
| 主題                                                                                                                                            | Description                                                                                                                                                                                                                                                          |
| ------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [使用基本資料類型](../../connect/jdbc/using-basic-data-types.md)                                                                           | 描述 JDBC 基本資料類型。 包括如何透過結果集、參數化查詢以及預存程序來使用資料類型的範例。                                                                                                        |
| [設定 java.sql.Time 值如何傳送給伺服器](../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md) | 描述 JDBC 驅動程式產生日期的方式。                                                                                                                                                                                                                       |
| [使用進階資料類型](../../connect/jdbc/using-advanced-data-types.md)                                                                     | 描述 JDBC 進階資料類型。                                                                                                                                                                                                                              |
| [了解資料類型差異](../../connect/jdbc/understanding-data-type-differences.md)                                                 | 描述各種 JDBC 驅動程式資料類型之間的差異。                                                                                                                                                                                                    |
| [了解資料類型轉換](../../connect/jdbc/understanding-data-type-conversions.md)                                                 | 描述在使用 getter 和 setter 方法時，如何處理資料類型轉換。                                                                                                                                                                                  |
| [國家字元集支援](../../connect/jdbc/national-character-set-support.md)                                                           | 描述國家字元集類型的支援。                                                                                                                                                                                                          |
| [支援 XML 資料](../../connect/jdbc/supporting-xml-data.md)                                                                                 | 描述 SQLXML 介面。 同時描述如何在具有 **SQLXML** Java 資料類型的關聯式資料庫中讀取和寫入 XML 資料。                                                                                                             |
| [包裝函式與介面](../../connect/jdbc/wrappers-and-interfaces.md)                                                                         | 討論擁有 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 特定方法與常數的介面，讓應用程式伺服器建立類別的 Proxy。同時討論 `java.sql.Wrapper` 介面的支援。 |
  
## <a name="see-also"></a>另請參閱

[JDBC Driver 概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
