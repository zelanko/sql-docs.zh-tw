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
manager: craigg
ms.openlocfilehash: ec549f256caeab598f6e49632b2a50cfa5841710
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63244622"
---
# <a name="odbc-jet-error-messages"></a>ODBC Jet 錯誤訊息
資料來源中發生的錯誤，ODBC 驅動程式會傳回錯誤訊息傳回給它 ODBC 檔案程式庫。 對於 ODBC 驅動程式或驅動程式管理員中發生的錯誤，驅動程式會傳回錯誤訊息會根據文字相關聯的 SQLSTATE。  
  
 錯誤訊息的格式如下：  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 括號 ([]) 中的前置詞會識別錯誤的位置。 當錯誤發生在驅動程式管理員 中，*資料來源*未指定。 當錯誤是發生在資料來源，[*廠商*] 和 [*ODBC 元件*] 前置詞識別供應商並收到錯誤，從資料來源的 ODBC 元件名稱。  
  
 下表顯示驅動程式管理員和驅動程式 ISAM 所傳回的錯誤訊息：  
  
|錯誤訊息|錯誤的位置|  
|-------------------|--------------------|  
|[Microsoft][ODBC 驅動程式管理員]*訊息文字*|驅動程式管理員 (Odbc32.dll)|  
|[Microsoft][ODBC *driver-name*]*message-text*|驅動程式 ISAM （請參閱驅動程式 ISAMs）|
