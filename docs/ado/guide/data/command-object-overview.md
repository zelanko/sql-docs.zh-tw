---
description: Command 物件概觀
title: 命令物件總覽 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- command object [ADO]
ms.assetid: e84a14b1-3c2a-4f7d-a966-9e08a93948df
author: rothja
ms.author: jroth
ms.openlocfilehash: d44c727a69dc74bf243bc2f2c0204cb41cd9f585
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453680"
---
# <a name="command-object-overview"></a>Command 物件概觀
使用 **命令** 物件，您可以執行下列動作：  
  
-   定義命令的可執行文字 (例如，使用 **CommandText** 屬性) 的 SQL 語句或預存程式。  
  
-   使用 **參數** 物件和 **Parameters** 集合來定義參數化查詢或預存程式引數。  
  
-   執行命令，並使用**Execute**方法傳回**記錄集**物件（如果有的話）。  
  
-   在執行之前使用 **CommandType** 屬性來指定命令類型，以優化效能。  
  
-   使用**命令**物件的 [**方言**] 屬性來指定有關命令文字的特定資訊。  
  
-   使用 **備** 妥的屬性，控制提供者是否要在執行之前儲存備妥的 (或編譯的) 版本的命令。  
  
-   使用 **CommandTimeout** 屬性，設定提供者將等待命令執行的秒數。  
  
-   藉由設定**ActiveConnection**屬性，將開啟的連接與**命令**物件產生關聯。  
  
-   設定 **Name** 屬性，將 **命令** 物件識別為相關聯 **連接** 物件上的方法。  
  
-   將**命令**物件傳遞至**記錄集**的**來源**屬性，以便取得資料。  
  
-   傳遞包含命令的 **資料流程** 物件 (例如，XML 命令) 給支援的提供者。
