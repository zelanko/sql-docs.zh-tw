---
description: 設定認可模式
title: 設定認可模式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
ms.assetid: b60d0d74-0655-4013-8d5a-bc1866eaa166
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a71d6f97f4683f9177c940be7d6ca1cc4a27c01
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494622"
---
# <a name="setting-the-commit-mode"></a>設定認可模式
應用程式會使用 SQL_ATTR_AUTOCOMMIT 連接屬性來指定交易模式。 依預設，除非不支援 **SQLSetConnectAttr** 和 **SQLSetConnectOption**) ，否則 ODBC 交易會處於自動認可模式 (。 從手動認可模式切換為自動認可模式時，會自動認可連線上任何開啟的交易。
