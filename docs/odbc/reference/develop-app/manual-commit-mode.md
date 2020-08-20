---
description: 手動認可模式
title: 手動認可模式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- manual-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: 9c4b3931-e48b-4960-89a2-5697537e9f51
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb576166242078707846e005b958143812fd5901
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499832"
---
# <a name="manual-commit-mode"></a>手動認可模式
*在手動認可模式中，* 應用程式必須藉由呼叫 **SQLEndTran** 來認可或回復交易，以明確完成交易。 這是大部分關係資料庫的一般交易模式。  
  
 ODBC 中的交易不需要明確起始。 相反地，每當應用程式在資料庫上開始操作時，就會隱含地開始交易。 如果資料來源需要明確的交易初始，驅動程式必須在應用程式執行需要交易的語句，而且沒有目前的交易時提供它。
