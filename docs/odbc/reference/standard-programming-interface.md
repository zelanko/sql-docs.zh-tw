---
title: 標準程式設計介面 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], programming interface
- programming interface standardization [ODBC]
ms.assetid: a2fa727e-51f2-4123-ae25-0ee28e611231
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c7767f113d0f70569ce253f0200cd35cb83915a4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81279994"
---
# <a name="standard-programming-interface"></a>標準程式設計介面
程式設計介面可能是標準化最明顯的候選方案。 事實上,在開發 ODBC 時,ANSI 和 ISO 已經為嵌入式 SQL 和 SQL 模組提供了標準。 雖然沒有資料庫 CLI 的標準,但 SQL Access 組(一個由資料庫供應商組成的產業聯盟)正在考慮是否創建資料庫 CLI;ODBC的一部分後來成為他們工作的基礎。  
  
 ODBC 的要求之一是單個應用程式二進位檔案必須使用多個 DBMS。 因此,ODBC 不使用嵌入式 SQL 或模組語言。 儘管嵌入式 SQL 和模組語言中的語言是標準化的,但每個語言都與特定於 DBMS 的預編譯器相關聯。 因此,必須為每個 DBMS 重新編譯應用程式,生成的二進位檔僅使用單個 DBMS。 雖然這適用於小型電腦和大型機世界中的低容量應用,但在個人電腦世界中是不能接受的。 首先,向客戶交付多個版本的大批量、收縮包裝軟體是一場後勤噩夢;其次,個人計算機應用程式通常需要同時訪問多個 DBMS。  
  
 另一方面,調用級介面可以通過駐留在每個本地計算機上的庫或資料庫驅動程序實現;每個 DBMS 都需要不同的驅動程式。 由於現代操作系統可以在運行時載入此類庫(如 Microsoft® Windows ® 操作系統上的動態連結庫),因此單個應用程式無需重新編譯即可訪問來自不同 DBMS 的數據,還可以同時從多個資料庫存取數據。 隨著新的資料庫驅動程式可用,使用者只需在其電腦上安裝這些驅動程式,而無需修改、重新編譯或重新連結其資料庫應用程式。 此外,調用級介面是 ODBC 的一個很好的候選點,因為 Windows(最初開發 ODBC 的平臺)已經廣泛使用了此類庫。
