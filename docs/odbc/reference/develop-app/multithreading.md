---
description: 多執行緒
title: 多執行緒 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], thread-safe
- thread-safe drivers [ODBC]
- multithreaded applications [ODBC]
ms.assetid: cdfebdf5-12ff-4e28-8055-41f49b77f664
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 470a3d3a4d76ae038e3c80b9aa9b93dfd1d0ed79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429240"
---
# <a name="multithreading"></a>多執行緒
在多執行緒作業系統上，驅動程式必須是安全線程。 也就是說，應用程式必須能夠在一個以上的執行緒上使用相同的控制碼。 達成此目的的方式是驅動程式特定的，而且驅動程式可能會將嘗試同時在兩個不同的執行緒上使用相同的控制碼序列化。  
  
 應用程式通常會使用多個執行緒，而不是非同步處理。 應用程式會建立個別的執行緒，並在其上呼叫 ODBC 函數，然後繼續在主執行緒上處理。 不需要持續輪詢非同步函式，就像使用 SQL_ATTR_ASYNC_ENABLE 語句屬性的情況一樣，應用程式可以讓新建立的執行緒完成。  
  
 接受語句控制碼並在一個執行緒上執行的函式，可以藉由呼叫 **SQLCancel** 與另一個執行緒的相同語句控制碼來取消。 雖然驅動程式不應該以這種方式序列化使用 **SQLCancel** ，但並不保證呼叫 **SQLCancel** 會實際取消在另一個執行緒上執行的函式。
