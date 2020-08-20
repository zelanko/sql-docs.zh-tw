---
description: 呼叫 SQLCloseCursor
title: 呼叫 SQLCloseCursor |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], SQLCloseCursor
- backward compatibility [ODBC], SqlCloseCursor
- SQLCloseCursor function [ODBC], calling
- upgrading applications [ODBC], SQLCloseCursor
- compatibility [ODBC], SQLCloseCursor
ms.assetid: ef448c39-a9ad-4f07-8ef3-65bd4cef672a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 925617d79266f0b50ef9b38586b31af91311b63e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494768"
---
# <a name="calling-sqlclosecursor"></a>呼叫 SQLCloseCursor
由於 **SQLCloseCursor** 與 SQL_CLOSE 的 **SQLFreeStmt** 幾乎相同，因此驅動程式管理員不會對應此函式。 取代函式已對應，因此*現有的 odbc* *2.x 應用程式*可以使用新函數輕鬆地移至 ODBC 3.x。 這類移動可讓這類應用程式更容易以模組化的方式，在條件式程式碼內開始使用新*的 ODBC 3.x 功能。* **SQLCloseCursor** 並不代表任何新功能。 從具有 SQL_CLOSE 的**SQLFreeStmt**移至**SQLCloseCursor** ，應用程式不會獲得任何優點。
