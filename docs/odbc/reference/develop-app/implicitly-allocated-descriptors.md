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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 271d479a9d2faa8cd7ab01e02e830b194c4138b2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300128"
---
# <a name="implicitly-allocated-descriptors"></a>隱含配置描述項
配置語句控制碼時，應用程式會隱含配置一組四個描述元。 應用程式可以取得這些隱含配置描述元的控制碼，做為語句控制碼的屬性。 當應用程式釋放語句控制碼時，驅動程式會釋出該控制碼上所有隱含配置的描述元。
