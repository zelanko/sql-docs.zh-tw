---
description: 自訂應用程式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56829c72264ba128554af0534e8a6bfa16254142
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429390"
---
# <a name="custom-applications"></a>自訂應用程式
自訂應用程式通常會對一些 Dbms 執行特定工作。 例如，應用程式可能會從單一 DBMS 取出資料並產生報表，或可能會在數個 Dbms 之間傳輸資料。 這些應用程式的共通之處是，在撰寫應用程式之前已知這些 Dbms，而且不太可能會在應用程式的存留期內變更。  
  
 因此，自訂應用程式需要很少或沒有任何互通性。 應用程式開發人員可以為每個 DBMS 和程式碼直接選擇單一驅動程式。 應用程式可以安全地包含驅動程式特定的程式碼，以利用這些驅動程式的功能，甚至可能呼叫原生資料庫 API 來使用 ODBC 不支援的功能。  
  
 大部分自訂應用程式的主要互通性問題是目標 Dbms 未來是否會變更。 若是如此，您可以撰寫更具互通性的程式碼來開始簡化這個程式。 不過，這類 Dbms 的變更很罕見，通常需要大量的工作。 因此，自訂應用程式的開發人員很少會選擇提高互通性的功能，它們通常會選擇在變更 Dbms 時，對該功能進行編碼。
