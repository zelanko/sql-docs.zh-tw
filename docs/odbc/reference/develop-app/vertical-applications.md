---
title: 垂直應用 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], vertical applications
- vertical applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: d50ea3e6-7a9e-4fb6-8cd8-1d429d2f7b3c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cc88f38fd1ffe8b2ee0033ad0a2abc4f15fd5cf3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300373"
---
# <a name="vertical-applications"></a>垂直應用程式
垂直應用程式通常針對單個 DBMS 執行定義良好的任務。 例如,訂單輸入應用程序跟蹤公司中的訂單。 這些類型的應用程式有共同之處是,資料庫架構通常由應用程式開發人員設計,雖然應用程式可能使用許多不同的 DBMS,但它適用於單個客戶的單個 DBMS。  
  
 由於垂直應用程式通常需要某些功能(如可滾動遊標或事務),因此它們很少支援所有 DBMS。 相反,它們往往在有限的 DBMS 集中高度互通。 通常,垂直應用程式開發人員選擇支援那些代表市場很大一部分並忽略其餘部分的 DBMS。 他們甚至可能選擇支援這些 DBMS 的特定驅動程式,以降低其測試和產品支援成本。  
  
 由於垂直應用程式可以支援一組已知的DBMS,因此它們有時包含特定於驅動程式或特定於DBMS的代碼。 但是,最好將此類代碼保持在最低限度,因為它需要額外的時間來維護。
