---
description: 取得描述項控制代碼
title: 取得描述項控制碼 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c46ce0bff7240c121c6c56a5c3cd1b19769afb04
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429200"
---
# <a name="obtaining-descriptor-handles"></a>取得描述項控制代碼
應用程式會取得任何明確配置描述項的控制碼，作為 **SQLAllocHandle**呼叫的輸出引數。 隱含配置描述項的控制碼是藉由呼叫 **SQLGetStmtAttr**來取得。
