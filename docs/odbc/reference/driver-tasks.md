---
title: "驅動程式工作 |Microsoft 文件"
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
- ODBC architecture [ODBC], drivers
- drivers [ODBC], tasks
ms.assetid: 184c795a-c2e8-4d20-9902-12e60b2f0e45
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 331e3aee3a4a60cbfa1a1308b71da80bf9772f23
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="driver-tasks"></a>驅動程式工作
特定驅動程式所執行的工作包括：  
  
-   連接與中斷連接資料來源。  
  
-   檢查函式不會檢查驅動程式管理員的錯誤。  
  
-   起始的交易。這是對應用程式。  
  
-   正在提交 SQL 陳述式來執行的資料來源。 驅動程式必須修改以 DBMS 專用 SQL; ODBC SQL這通常是有限取代以 DBMS 專用的 SQL ODBC 所定義的逸出子句。  
  
-   將資料傳送到和擷取資料來源的資料，包括將應用程式所指定的資料類型轉換。  
  
-   對應至 ODBC Sqlstate DBMS 特定錯誤。
