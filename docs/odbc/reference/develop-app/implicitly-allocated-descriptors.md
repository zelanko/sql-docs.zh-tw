---
title: 隱含地配置描述元 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- implicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 9f88c863-affc-4ab4-a558-63a3ef766f37
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d805b110453c5fe0bb5be8c8df067c09ff8146e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913873"
---
# <a name="implicitly-allocated-descriptors"></a>隱含地配置描述元
當配置陳述式控制代碼時，應用程式以隱含方式配置一組的四個描述項。 應用程式可以取得這些隱含地配置描述元做為屬性的陳述式控制代碼的控制代碼。 當應用程式會釋放陳述式控制代碼時，驅動程式會釋放該控制代碼上的所有隱含地配置描述元。
