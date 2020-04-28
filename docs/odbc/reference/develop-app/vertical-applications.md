---
title: 垂直應用程式 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300373"
---
# <a name="vertical-applications"></a>垂直應用程式
垂直應用程式通常會針對單一 DBMS 執行妥善定義的工作。 例如，訂單輸入應用程式會追蹤公司中的訂單。 這些類型的應用程式通常是由應用程式開發人員所設計，而應用程式可能會使用多個不同的 Dbms，它適用于單一客戶的單一 DBMS。  
  
 由於垂直應用程式通常需要特定的功能，例如可滾動的資料指標或交易，因此很少會支援所有 Dbms。 相反地，它們通常會在一組有限的 Dbms 之間具有高互通性。 一般而言，垂直應用程式開發人員會選擇支援那些代表大量市場的 Dbms，並忽略其餘部分。 他們甚至可能會選擇支援這些 Dbms 的特定驅動程式，以降低其測試和產品支援成本。  
  
 由於垂直應用程式可以支援一組已知的 Dbms，因此有時會包含特定驅動程式或 DBMS 專屬的程式碼。 不過，這類程式碼最好保持最小狀態，因為它需要額外的時間來維護。
