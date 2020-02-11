---
title: 隱含配置的描述元 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138949"
---
# <a name="implicitly-allocated-descriptors"></a>隱含配置描述項
配置語句控制碼時，應用程式會隱含配置一組四個描述元。 應用程式可以取得這些隱含配置描述元的控制碼，做為語句控制碼的屬性。 當應用程式釋放語句控制碼時，驅動程式會釋出該控制碼上所有隱含配置的描述元。
