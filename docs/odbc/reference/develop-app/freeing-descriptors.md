---
title: 釋放描述項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
- descriptors [ODBC], allocating and freeing
- freeing descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 317213f4-0ebb-4bf8-a37a-4d6b1313823f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d643ccad0110796127524a10e82aef7c3339b163
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694626"
---
# <a name="freeing-descriptors"></a>釋放描述項
明確配置描述元可以是藉由呼叫其中一個明確地釋放**SQLFreeHandle**具有*HandleType* SQL_HANDLE_DESC，或以隱含的方式，當連接控制代碼釋放。 明確配置描述項會釋放時，要自動套用的釋放描述項會還原為隱含地配置給它們的描述元的所有陳述式控制代碼。  
  
 隱含配置描述項可以只藉由呼叫釋放**SQLDisconnect**，會卸除任何陳述式，或描述開啟連線時，或藉由呼叫**SQLFreeHandle**使用*HandleType*來釋放陳述式控制代碼和陳述式相關聯的所有隱含配置描述項的利用 SQL_HANDLE_STMT。 無法釋放隱含配置描述元，藉由呼叫**SQLFreeHandle**具有*HandleType* SQL_HANDLE_DESC。  
  
 即使在釋出，隱含配置描述元會維持有效，並**SQLGetDescField**可呼叫它的欄位。
