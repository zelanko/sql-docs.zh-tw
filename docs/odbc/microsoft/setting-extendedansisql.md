---
title: 設定擴展安西SQL |微軟文件
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
ms.openlocfilehash: 6b5c2e4ed4d8bd64d02fb6a62861db832f6b0898
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300798"
---
# <a name="setting-extendedansisql"></a>設定 ExtendedAnsiSQL
可以透過新增延伸 AnsiSQL 屬性在連接字串中控制該屬性:  
  
|值|描述|  
|-----------|-----------------|  
|延伸安西SQL=0(預設)|此設定無法啟用新功能。|  
|擴展安西SQL_1|此設置啟用新功能。|  
  
 在透過控制面板配置 DSN 時,還可以透過 **「進階選項」** 對話框在 DSN 中設定該屬性。  
  
 將屬性設置為 0 會禁用新功能;將其設置為 1 啟用新功能。  
  
 也可以使用 SQLSetConnectAttr() 設置該屬性。 屬性值為 65501,並設置為 SQLINTEGER 值 1 或 0,如上表所述。 它可以在連接之前或之後調用,但最好在連接後調用它,因為驅動程式處理緩存的連接屬性和連接字串的順序。
