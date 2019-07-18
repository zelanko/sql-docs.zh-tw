---
title: Jet 4.0 會使用 SQL-92 保留的字清單時在 ExtendedAnsiSQL_Set |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], reserved words
ms.assetid: 7645187e-7777-4c07-9686-0a80d5c5834d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 93d23216db950ed861449061f3e35e5e88a637fb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058790"
---
# <a name="jet-40-uses-sql-92-reserved-words-list-when-extendedansisqlset"></a>Jet 4.0 在 ExtendedAnsiSQL_Set 時使用 SQL-92 保留字清單
當開啟 ExtendedAnsiSQL 旗標時，Jet 4.0 會使用 SQL-92 保留的字清單。 嘗試使用 SQL-92 保留字，因為不具引號的物件名稱會導致語法錯誤。 ExtendedAnsiSQL 旗標已關閉時，新的保留的字可用來當做為之前的物件名稱中。
