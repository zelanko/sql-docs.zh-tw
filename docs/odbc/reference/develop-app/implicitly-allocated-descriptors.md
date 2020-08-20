---
description: 隱含配置描述項
title: 隱含配置的描述項 |Microsoft Docs
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
ms.openlocfilehash: 5daa7f622798e1394c186b333069933b48e367af
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461420"
---
# <a name="implicitly-allocated-descriptors"></a>隱含配置描述項
配置語句控制碼時，應用程式會隱含配置一組四個描述項。 應用程式可以取得這些隱含配置描述元的控制碼，作為語句控制碼的屬性。 當應用程式釋放語句控制碼時，驅動程式會釋出該控制碼上所有隱含配置的描述項。
