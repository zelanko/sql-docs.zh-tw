---
description: 設定 ExtendedAnsiSQL
title: 設定 ExtendedAnsiSQL |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], setting
ms.assetid: 37b775d1-65ac-45ac-8572-454bc4e3c1a2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5a2d739a3093b0d1e806bc9aa3f8d136746954c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412444"
---
# <a name="setting-extendedansisql"></a>設定 ExtendedAnsiSQL
您可以藉由新增 ExtendedAnsiSQL 屬性，在連接字串中控制此屬性：  
  
|值|描述|  
|-----------|-----------------|  
|ExtendedAnsiSQL = 0 (預設) |此設定不會啟用新的功能。|  
|ExtendedAnsiSQL = 1|此設定可啟用新功能。|  
  
 透過主控台設定 DSN 時，也可以透過 [ **Advanced Options** ] 對話方塊設定此屬性。  
  
 將屬性設定為0會停用新功能;將它設定為1可啟用新功能。  
  
 也可以使用 SQLSetConnectAttr ( # A1 來設定屬性。 屬性值為65501，且設定為 SQLINTEGER 值1或0，如上表所述。 您可以在連接之前或之後呼叫它，但是最好在連接之後呼叫它，因為驅動程式處理快取的連接屬性和連接字串的順序。
