---
title: 垂直應用程式 |Microsoft 文件
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
- interoperability [ODBC], vertical applications
- vertical applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: d50ea3e6-7a9e-4fb6-8cd8-1d429d2f7b3c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f71f960043a843c2aad5f7e3a7eb5cc997b0a6ed
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="vertical-applications"></a>垂直應用程式
垂直應用程式通常會執行完整定義的工作，針對單一 DBMS。 例如，訂單輸入應用程式會追蹤在公司的訂單。 什麼這些類型的應用程式都有通用是通常會由應用程式開發人員設計用資料庫結構描述，當應用程式可能使用的不同 Dbms 的數字，它使用單一的 DBMS 單一客戶。  
  
 垂直應用程式通常需要特定的功能，例如可捲動資料指標或交易，因為它們很少會支援所有 Dbms。 相反地，它們通常會在一組有限的 Dbms 之間具備高度互通性。 一般而言，垂直應用程式開發人員選擇支援那些 Dbms，表示市場的大型分數而忽略其餘複本。 他們甚至可能會選擇特定驅動程式支援這些以減少其測試的 Dbms 和產品支援成本。  
  
 垂直應用程式都能支援一組已知的 Dbms，他們有時會包含特定驅動程式或 DBMS 專屬的程式碼。 不過，這類程式碼是最佳保持在最低限度因為它需要額外的時間來維護。
