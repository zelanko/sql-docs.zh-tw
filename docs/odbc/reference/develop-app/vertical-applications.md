---
description: 垂直應用程式
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
ms.openlocfilehash: a12be9247af3f273526dd08ee99ff7cc301af822
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421402"
---
# <a name="vertical-applications"></a>垂直應用程式
垂直應用程式通常會對單一 DBMS 執行妥善定義的工作。 例如，訂單輸入應用程式會追蹤公司中的訂單。 這些類型的應用程式最常見的情況是，資料庫架構通常是由應用程式開發人員所設計，而應用程式可能會使用許多不同的 Dbms，而單一客戶可以使用單一 DBMS。  
  
 因為垂直應用程式通常需要特定的功能，例如可滾動的資料指標或交易，所以很少支援所有 Dbms。 相反地，它們通常會在一組有限的 Dbms 之間具互通性。 一般的應用程式開發人員通常會選擇支援那些代表一小部分市場的 Dbms，並忽略其餘部分。 他們甚至可以選擇支援這些 Dbms 的特定驅動程式，以降低其測試和產品支援成本。  
  
 因為垂直應用程式可以支援一組已知的 Dbms，所以有時會包含驅動程式特定或 DBMS 特定的程式碼。 不過，這類程式碼最好保持最小狀態，因為它需要額外的時間來維護。
