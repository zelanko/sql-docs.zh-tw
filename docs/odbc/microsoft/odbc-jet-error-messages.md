---
title: ODBC 噴射錯誤消息 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8fa6e672b69c7791e66dc3919e6fcd22b7c3de7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293108"
---
# <a name="odbc-jet-error-messages"></a>ODBC Jet 錯誤訊息
對於資料來源中發生的錯誤,ODBC 驅動程式將返回由 ODBC 檔庫返回的錯誤訊息。 對於在 ODBC 驅動程式或驅動程式管理器中發生的錯誤,驅動程式會返回一條錯誤消息,該錯誤消息基於與 SQLSTATE 關聯的文本。  
  
 錯誤訊息具有以下格式:  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 括號 (* +) 中的前置碼的識別錯誤的位置。 當驅動程式管理員發生錯誤時,不會給出*資料來源*。 當資料來源中發生錯誤時, [*供應商*] 和 [*ODBC- 元件*] 前碼從資料來源接收錯誤的 ODBC 元件的供應商和名稱。  
  
 下表顯示驅動程式管理器和驅動程式 ISAM 傳回的錯誤訊息:  
  
|錯誤訊息|錯誤位置|  
|-------------------|--------------------|  
|[微軟][ODBC 驅動程式管理員]*訊息文字*|駕駛員管理員 (Odbc32.dll)|  
|[微軟][ODBC*驅動程式名稱*]*訊息文字*|驅動程式 ISAM(請參考驅動程式 ISAM)|
