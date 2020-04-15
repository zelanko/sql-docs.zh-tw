---
title: 基於 DBMS 的驅動程式 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drivers [ODBC], DBMS-based drivers
- DBMS-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
ms.assetid: e2208ee0-4cd6-4f0d-bb71-a0b54f7d9330
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4e7b7b153d0b0cb0a3e6a3d738908b0039b95679
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306484"
---
# <a name="dbms-based-drivers"></a>以 DBMS 為基礎的驅動程式
基於 DBMS 的驅動程式與資料來源(如 Oracle 或 SQL Server)一起使用,這些資料來源提供獨立資料庫引擎供驅動程式使用。 這些驅動程式通過獨立引擎訪問物理數據;也就是說,它們向引擎提交 SQL 語句並從引擎中檢索結果。  
  
 由於基於 DBMS 的驅動程式使用現有的資料庫引擎,因此它們通常比基於檔的驅動程式更易於寫入。 儘管通過將 ODBC 調用轉換為本機 API 調用可以輕鬆實現基於 DBMS 的驅動程式,但這將導致驅動程式變慢。 實現基於 DBMS 的驅動程式的更好方法是使用基礎數據流協定,這通常是本機 API 的作用。 例如,SQL Server 驅動程式應使用 TDS(SQL Server 的數據流協定),而不是資料庫庫(SQL Server 的本機 API)。 此規則的一個例外是當 ODBC 是本機 API 時。 例如,Watcom SQL 是一個獨立的引擎,它駐留在與應用程式相同的計算機上,並且直接作為驅動程式載入。  
  
 基於 DBMS 的驅動程式充當用戶端/伺服器配置中的用戶端,數據來源在其中充當伺服器。 在大多數情況下,用戶端(驅動程式)和伺服器(數據源)駐留在不同的計算機上,儘管兩者可以駐留在運行多任務操作系統的同一台計算機上。 第三種可能性是*閘道,* 它位於驅動程式和資料源之間。 閘道是使一個 DBMS 看起來像另一個軟體。 例如,編寫用於 SQL Server 的應用程式還可以透過微決策軟體 DB2 閘道存取 DB2 資料;此產品使 DB2 看起來像 SQL 伺服器。  
  
 下圖顯示了基於 DBMS 的驅動程式的三種不同配置。 在第一個配置中,驅動程式和數據源駐留在同一台計算機上。 在第二個中,驅動程式和數據源駐留在不同的計算機上。 在第三個中,驅動程式和數據源駐留在不同的計算機上,閘道位於它們之間,駐留在另一台電腦上。  
  
 ![基於 DBMS&#45;驱动程序的三种配置](../../odbc/reference/media/pr07.gif "pr07")
