---
title: SQLSpecialColumns （桌面資料庫驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Desktop Database Drivers
ms.assetid: 3de66fdf-053b-4354-979d-e76a5a5e975f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e530d0b16811cdf25a5bc1d99f5386efdb55ccd4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905322"
---
# <a name="sqlspecialcolumns-desktop-database-drivers"></a>SQLSpecialColumns (桌面資料庫驅動程式)
系統會針對*fColType*中的 SQL_BEST_ROWID 旗標，傳回唯一索引（如果有的話）。 SQL_ROWVER 旗標不會傳回任何結果集。  
  
 所有資料列識別碼的範圍都是 SQL_SCOPE_CURROW。  
  
 *SzTableQualifier*或*szTableName*引數不支援模式比對。
