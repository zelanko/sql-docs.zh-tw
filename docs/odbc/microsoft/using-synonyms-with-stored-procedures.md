---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6e798a9c7fa3365082a2e6dab562596d56649ec4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088017"
---
# <a name="using-synonyms-with-stored-procedures"></a>搭配使用同義字與預存程序
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 Microsoft ODBC Driver for Oracle 版本2.0 和2.5 在呼叫 Oracle 預存程式時，不支援同義字。 當與其他 Oracle 資料庫物件（例如資料表）搭配使用時，同義字會如預期般運作。
