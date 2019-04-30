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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: df7a2d036692cefcd1b2ea2338d51938a11ea85a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208431"
---
# <a name="vertical-applications"></a>垂直應用程式
垂直應用程式通常會執行完整定義的工作，針對單一 DBMS。 例如，訂單輸入應用程式會追蹤公司中的訂單。 什麼這些類型的應用程式有共通是資料庫結構描述通常設計用在應用程式開發人員，當應用程式可能會使用幾個不同的 Dbms 的它使用單一的 DBMS 單一客戶。  
  
 垂直應用程式通常會需要某些功能，例如可捲動資料指標或交易，因為它們很少會支援所有的 Dbms。 相反地，他們傾向於對一組有限的 Dbms 之間高度互通。 一般而言，垂直應用程式開發人員選擇支援這些代表極大部分的市場有所認識，並忽略其餘的 Dbms。 他們甚至可能會選擇這些 Dbms 來減少其測試和產品支援費用支援特定的驅動程式。  
  
 垂直應用程式，都能支援一組已知的 Dbms，有時會包含特定驅動程式或 DBMS 專屬的程式碼。 不過，這類程式碼是最能保持在最低限度因為它需要額外的時間來維護。
