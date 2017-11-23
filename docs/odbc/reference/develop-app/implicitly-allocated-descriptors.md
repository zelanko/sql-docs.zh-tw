---
title: "隱含地配置描述元 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- implicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 9f88c863-affc-4ab4-a558-63a3ef766f37
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a0018755a9a03cb84385f2a187fdb1d62f0f6244
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="implicitly-allocated-descriptors"></a>隱含地配置描述元
當配置陳述式控制代碼時，應用程式以隱含方式配置一組的四個描述項。 應用程式可以取得這些隱含地配置描述元做為屬性的陳述式控制代碼的控制代碼。 當應用程式會釋放陳述式控制代碼時，驅動程式會釋放該控制代碼上的所有隱含地配置描述元。
