---
title: 設定提交模式 |微軟文件
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
ms.openlocfilehash: f05aaca2349a612cda7c5b6b257e7a1d5a5ea9c5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299818"
---
# <a name="setting-the-commit-mode"></a>設定認可模式
應用程式使用SQL_ATTR_AUTOCOMMIT連接屬性指定事務模式。 默認情況下,ODBC 事務處於自動提交模式(除非不支援**SQLSetConnectAttr**和**SQLSetConnectOption,** 這不太可能)。 從手動提交模式切換到自動提交模式會自動提交連接上的任何未結事務。
