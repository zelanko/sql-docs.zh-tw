---
title: 明確配置描述元 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: fbec69e0d984d843abc2b8754e111a1199c79a5a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47644536"
---
# <a name="explicitly-allocated-descriptors"></a>明確配置描述項
應用程式可以明確地將配置隨時連線到資料庫的連接上的應用程式描述項。 藉由指定該描述元控制代碼，因為陳述式的屬性處理使用**SQLSetStmtAttr**，應用程式會引導驅動程式使用該描述元來取代對應以隱含方式配置應用程式描述元。 應用程式無法指定替代的實作描述項。  
  
 應用程式可以關聯多個陳述式的明確配置描述元。 只有在應用程式實際連接到資料庫時，才將描述元可以是明確配置描述項。 應用程式可以釋放描述項明確或隱含釋放它的連線。
