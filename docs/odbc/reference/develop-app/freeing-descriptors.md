---
title: 釋放描述符 |微軟文件
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
ms.openlocfilehash: af30ceb29e032764b89aa2069086aa898a7d35db
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305599"
---
# <a name="freeing-descriptors"></a>釋放描述項
顯式分配的描述符可以通過使用*SQL_HANDLE_DESC 的 HandleType*調用**SQLFreeHandle**或隱式釋放連接句柄時顯式釋放。 釋放顯式分配的描述符時,釋放的描述符應用的所有語句句柄將自動還原到隱式為其分配的描述符。  
  
 隱含式配置的描述符只能透過呼叫**SQLDisconnect**(它丟棄連接上打開的任何語句或描述符)來釋放,或者使用*handletype* SQL_HANDLE_STMT 呼叫**SQLFreeHandle**以釋放語句句柄以及與語句關聯的所有隱式分配的描述符。 無法透過使用*SQL_HANDLE_DESC的句柄類型*呼叫**SQLFreeHandle**來釋放隱式分配的描述符。  
  
 即使釋放,隱式分配的描述符仍然有效 **,SQLGetDescField**也可以在其欄位上調用。
