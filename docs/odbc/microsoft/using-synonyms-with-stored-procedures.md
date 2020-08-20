---
description: 搭配使用同義字與預存程序
title: 搭配使用同義字與預存程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 8620b039-a086-4534-8710-cc8b1787dc80
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6c0f210aad903dec6b29df2ca1bd121b569c4335
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471300"
---
# <a name="using-synonyms-with-stored-procedures"></a>搭配使用同義字與預存程序
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 當呼叫 Oracle 預存程式時，Microsoft ODBC Driver for Oracle 版本2.0 和2.5 不支援同義字。 同義字與其他 Oracle 資料庫物件（例如資料表）搭配使用時，會如預期般運作。
