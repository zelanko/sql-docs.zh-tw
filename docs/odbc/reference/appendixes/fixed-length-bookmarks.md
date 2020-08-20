---
description: 固定長度書籤
title: 固定長度書簽 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d357ba96141c658889628941c7f9492db5fd6b66
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466174"
---
# <a name="fixed-length-bookmarks"></a>固定長度書籤
如果 ODBC 3.x *驅動程式* 應該搭配使用固定長度書簽的 odbc 2.x *應用程式* 使用，則驅動程式必須支援下列各項：  
  
-   SQL_UB_ON 做為 SQL_USE_BOOKMARKS 語句選項的值。  (SQL_UB_ON 已*在 ODBC 3.x 中淘汰。 ) *  
  
-   SQL_GET_BOOKMARK 語句選項。
