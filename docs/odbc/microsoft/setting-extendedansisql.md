---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c9b8999e229e8a6ed4804b2f06a4072d139ae93a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47818150"
---
# <a name="setting-extendedansisql"></a>設定 ExtendedAnsiSQL
屬性可以控制的連接字串中，藉由新增 ExtendedAnsiSQL 屬性：  
  
|值|描述|  
|-----------|-----------------|  
|ExtendedAnsiSQL = 0 （預設值）|此設定不會啟用新功能。|  
|ExtendedAnsiSQL = 1|此設定可讓新的功能。|  
  
 屬性也可以設定透過 dsn**進階選項**時設定 DSN 中的，透過 [控制台] 對話方塊。  
  
 將屬性設定為 0 會停用新的功能;將它設定為 1 會啟用新功能。  
  
 屬性也可以使用 SQLSetConnectAttr() 來設定。 屬性值是 65501，並設定為 SQLINTEGER 值為 1 或 0，在上表中所述。 它可呼叫之前或之後連接，但最好是呼叫因為順序的驅動程式處理程序快取的連接屬性和連接字串連接之後。
