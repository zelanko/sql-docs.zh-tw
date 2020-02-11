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
ms.openlocfilehash: 330b55ef2d4fee090c453990d3fe75e6e2dacb6f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063604"
---
# <a name="setting-extendedansisql"></a>設定 ExtendedAnsiSQL
藉由新增 ExtendedAnsiSQL 屬性，可以在連接字串中控制屬性：  
  
|值|描述|  
|-----------|-----------------|  
|ExtendedAnsiSQL = 0 （預設值）|此設定不會啟用新功能。|  
|ExtendedAnsiSQL = 1|此設定可啟用新功能。|  
  
 透過 [控制台] 設定 DSN 時，也可以透過 [ **Advanced Options** ] 對話方塊，在 DSN 中設定屬性。  
  
 將屬性設定為0會停用新功能;將它設定為1可啟用新功能。  
  
 您也可以使用 SQLSetConnectAttr （）來設定屬性。 屬性值為65501，而且設定為1或0的 SQLINTEGER 值，如上表所述。 您可以在連接之前或之後呼叫它，但最好在連接後呼叫它，因為驅動程式處理快取的連接屬性和連接字串的順序。
