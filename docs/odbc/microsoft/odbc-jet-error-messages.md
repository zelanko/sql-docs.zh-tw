---
title: ODBC Jet 錯誤訊息 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages (ODBC driver for oracle)
ms.assetid: f8d2a8f2-0316-42c4-bc34-5367661634ae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85e0f9a8bc7015a0ad5b12ce46a6c94ab31ca43c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915808"
---
# <a name="odbc-jet-error-messages"></a>ODBC Jet 錯誤訊息
對於發生在資料來源中的錯誤，ODBC 驅動程式會傳回 ODBC 檔案程式庫傳回的錯誤訊息。 對於 ODBC 驅動程式或驅動程式管理員中發生的錯誤，驅動程式會根據與 SQLSTATE 相關聯的文字傳回錯誤訊息。  
  
 錯誤訊息的格式如下：  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 以方括弧（[]）括住的首碼可識別錯誤的位置。 當驅動程式管理員中發生錯誤時，不會提供*資料來源*。 當資料來源發生錯誤時，[*廠商*] 和 [*ODBC 元件*] 前置詞會識別從資料來源收到錯誤之 ODBC 元件的廠商和名稱。  
  
 下表顯示驅動程式管理員和驅動程式 ISAM 所傳回的錯誤訊息：  
  
|錯誤訊息|錯誤位置|  
|-------------------|--------------------|  
|Microsoft[ODBC 驅動程式管理員]*message-text*|驅動程式管理員（Odbc32.lib .dll）|  
|Microsoft[ODBC*驅動程式-名稱*]*message-text*|驅動程式 ISAM （請參閱驅動程式 ISAMs）|
