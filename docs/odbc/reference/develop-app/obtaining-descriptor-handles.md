---
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
ms.openlocfilehash: c17b693080c2727d2ee788b74f247d86d7a3cb27
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302343"
---
# <a name="obtaining-descriptor-handles"></a>取得描述項控制代碼
應用程式會取得任何明確配置之描述元的控制碼，做為呼叫**SQLAllocHandle**的輸出引數。 隱含配置描述元的控制碼是藉由呼叫**SQLGetStmtAttr**取得。
