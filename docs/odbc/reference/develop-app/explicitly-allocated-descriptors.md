---
title: 明確配置的描述元 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- explicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: f590251d-56a6-4d58-a405-9e85e68fbc47
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5808265a9ab70b9947cea64fef790497c7229da8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069933"
---
# <a name="explicitly-allocated-descriptors"></a>明確配置描述項
應用程式可以在連接到資料庫時，于連線上明確地配置應用程式描述元。 藉由使用**SQLSetStmtAttr**將該描述項控制碼指定為語句控制碼的屬性，應用程式會指示驅動程式使用該描述項來取代對應的隱含配置應用程式描述元。 應用程式無法指定替代的執行描述項。  
  
 應用程式可以將明確配置的描述元與一個以上的語句產生關聯。 只有當應用程式實際連接到資料庫時，描述項才會是明確配置的描述項。 應用程式可以明確釋放這類描述元，或藉由釋放其連接來隱含地釋出。
