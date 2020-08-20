---
description: 明確配置描述項
title: 明確配置的描述項 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7215d17a7156419f08bbd73528c468d7b6355b94
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461480"
---
# <a name="explicitly-allocated-descriptors"></a>明確配置描述項
應用程式可以在連接至資料庫時，在連接上明確地配置應用程式描述項。 藉由使用 **SQLSetStmtAttr**將描述項控制碼指定為語句控制碼的屬性，應用程式會指示驅動程式使用該描述項來取代對應的隱含配置應用程式描述項。 應用程式無法指定替代的執行描述項。  
  
 應用程式可以將明確配置的描述項與一個以上的語句產生關聯。 只有當應用程式實際連接至資料庫時，描述項才能是明確配置的描述項。 應用程式可以明確地釋放這類描述項，或藉由釋放其連接來隱含地釋放。
