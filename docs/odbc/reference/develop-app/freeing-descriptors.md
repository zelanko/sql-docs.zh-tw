---
title: 釋放描述元 |Microsoft Docs
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
ms.openlocfilehash: fe489222c026c1499135b716f0485bb04f51bad9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069776"
---
# <a name="freeing-descriptors"></a>釋放描述項
明確配置的描述元可以藉由使用 SQL_HANDLE_DESC 的*HandleType*呼叫**SQLFreeHandle** ，或在連接控制碼釋放時隱含地釋放。 釋放明確配置的描述元之後，所有套用的已釋放描述元都會自動還原成隱含配置給它們的描述元。  
  
 隱含配置的描述元只能藉由呼叫**SQLDisconnect**來釋放，這會卸載在連接上開啟的任何語句或描述元，或使用 SQL_HANDLE_STMT 的*HandleType*呼叫**SQLFreeHandle**來釋放語句控制碼，以及與語句相關聯的所有隱含配置描述元。 以 SQL_HANDLE_DESC 的*HandleType*呼叫**SQLFreeHandle** ，無法釋放隱含配置的描述元。  
  
 即使在釋放時，隱含配置的描述元仍然有效，而且可以在其欄位上呼叫**SQLGetDescField** 。
