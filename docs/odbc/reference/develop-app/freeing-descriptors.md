---
description: 釋放描述項
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 95c87b7ac70369509a72ff539c63ac888e5f3262
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465800"
---
# <a name="freeing-descriptors"></a>釋放描述項
明確配置的描述元可以明確地釋放，方法是使用*HandleType*的 SQL_HANDLE_DESC 呼叫**SQLFreeHandle** ，或在釋放連接控制碼時隱含地釋放。 當已明確配置的描述項釋出時，已套用的已釋放描述元會自動還原成隱含配置給它們的描述項。  
  
 隱含配置的描述項只能透過呼叫**SQLDisconnect**來釋出，這會卸載在連接上開啟的任何語句或描述項，或透過 SQL_HANDLE_STMT 的*HandleType*來呼叫**SQLFreeHandle** ，以釋放語句控制碼以及與語句相關聯的所有隱含配置描述元。 以 SQL_HANDLE_DESC 的*HandleType*呼叫**SQLFreeHandle** ，無法釋放隱含配置的描述項。  
  
 即使在釋放時，隱含配置的描述項仍有效，而且可以在其欄位上呼叫 **SQLGetDescField** 。
