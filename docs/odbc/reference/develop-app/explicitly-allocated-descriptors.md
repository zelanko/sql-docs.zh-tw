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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9950bc23a1e75606316039e6c2d66f3dba59940
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305689"
---
# <a name="explicitly-allocated-descriptors"></a>明確配置描述項
應用程式可以在連接到資料庫時，于連線上明確地配置應用程式描述元。 藉由使用**SQLSetStmtAttr**將該描述項控制碼指定為語句控制碼的屬性，應用程式會指示驅動程式使用該描述項來取代對應的隱含配置應用程式描述元。 應用程式無法指定替代的執行描述項。  
  
 應用程式可以將明確配置的描述元與一個以上的語句產生關聯。 只有當應用程式實際連接到資料庫時，描述項才會是明確配置的描述項。 應用程式可以明確釋放這類描述元，或藉由釋放其連接來隱含地釋出。
