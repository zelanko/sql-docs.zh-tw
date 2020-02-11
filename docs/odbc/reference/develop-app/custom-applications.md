---
title: 自訂應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], custom applications
- custom applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: f28178d9-ecd6-4e8c-9644-9bb624999dcb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 240bdf074fbe7fd28f5aafff5c1bbab7651d0c71
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68067469"
---
# <a name="custom-applications"></a>自訂應用程式
自訂應用程式通常會針對幾個 Dbms 執行特定工作。 例如，應用程式可能會從單一 DBMS 抓取資料並產生報告，或可能會在數個 Dbms 間傳輸資料。 這些應用程式的常見之處在于，這些 Dbms 在撰寫應用程式之前是已知的，而且在應用程式的生命週期內可能不會變更。  
  
 因此，自訂應用程式需要很少或沒有互通性。 應用程式開發人員可以為每個 DBMS 和程式碼直接選擇一個驅動程式。 應用程式可以安全地包含驅動程式特有的程式碼，以利用這些驅動程式的功能，甚至可能呼叫原生資料庫 API 來使用 ODBC 所不支援的功能。  
  
 大部分自訂應用程式的主要互通性考慮是目標 Dbms 未來是否會變更。 若是如此，您可以撰寫更具互通性的程式碼來開始進行，藉此簡化此程式。 不過，這類 Dbms 的變更很罕見，通常需要大量的工作。 因此，自訂應用程式的開發人員很少會選擇增加功能的互通性;它們通常會選擇在變更 Dbms 時，再次編碼該功能。
