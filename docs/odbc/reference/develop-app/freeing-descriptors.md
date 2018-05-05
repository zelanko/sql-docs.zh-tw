---
title: 釋放描述 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
- descriptors [ODBC], allocating and freeing
- freeing descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 317213f4-0ebb-4bf8-a37a-4d6b1313823f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c96d5b654d8331f95e3abbe8a3aa8b563bf7a63
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="freeing-descriptors"></a>釋放描述元
明確配置描述元可以是明確地釋放是藉由呼叫**SQLFreeHandle**與*HandleType* SQL_HANDLE_DESC，或隱含的當連接控制代碼已釋放。 明確配置描述項會釋出，隱含地配置給它們的描述元釋放自動套用的描述元將還原的所有陳述式控制代碼。  
  
 隱含地配置描述元可以釋放只是藉由呼叫**SQLDisconnect**，會卸除任何陳述式，或描述開啟連接上，或藉由呼叫**SQLFreeHandle**與*HandleType*來釋放陳述式控制代碼和陳述式相關聯的所有隱含地配置描述元利用 SQL_HANDLE_STMT。 藉由呼叫，將無法釋放隱含地配置描述項**SQLFreeHandle**與*HandleType* SQL_HANDLE_DESC。  
  
 即使釋出，隱含地配置描述項會維持有效，以及**SQLGetDescField**可針對其欄位。
