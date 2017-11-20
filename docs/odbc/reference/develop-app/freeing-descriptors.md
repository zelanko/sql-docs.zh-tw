---
title: "釋放描述 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
- descriptors [ODBC], allocating and freeing
- freeing descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 317213f4-0ebb-4bf8-a37a-4d6b1313823f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d1c70c82196907fc0bd9747a8ece089d4e4ab514
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="freeing-descriptors"></a>釋放描述元
明確配置描述元可以是明確地釋放是藉由呼叫**SQLFreeHandle**與*HandleType* SQL_HANDLE_DESC，或隱含的當連接控制代碼已釋放。 明確配置描述項會釋出，隱含地配置給它們的描述元釋放自動套用的描述元將還原的所有陳述式控制代碼。  
  
 隱含地配置描述元可以釋放只是藉由呼叫**SQLDisconnect**，會卸除任何陳述式，或描述開啟連接上，或藉由呼叫**SQLFreeHandle**與*HandleType*來釋放陳述式控制代碼和陳述式相關聯的所有隱含地配置描述元利用 SQL_HANDLE_STMT。 藉由呼叫，將無法釋放隱含地配置描述項**SQLFreeHandle**與*HandleType* SQL_HANDLE_DESC。  
  
 即使釋出，隱含地配置描述項會維持有效，以及**SQLGetDescField**可針對其欄位。

