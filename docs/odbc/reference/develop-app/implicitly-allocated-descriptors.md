---
title: 隱含配置描述元 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- implicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 9f88c863-affc-4ab4-a558-63a3ef766f37
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c0eb34866b75802a32c63e62b41d384e5a1dea73
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138949"
---
# <a name="implicitly-allocated-descriptors"></a>隱含配置描述項
當配置陳述式控制代碼時，應用程式以隱含方式配置一組四個描述項。 應用程式可以取得這些隱含配置描述元，做為屬性的陳述式控制代碼的控制代碼。 當應用程式會釋放陳述式控制代碼時，驅動程式會釋放該控制代碼上的所有隱含配置描述項。
