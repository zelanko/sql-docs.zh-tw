---
description: ODBC Jet 錯誤訊息
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19f7d4b00c9e6b206ecd563083c0fcf16ced55e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340714"
---
# <a name="odbc-jet-error-messages"></a>ODBC Jet 錯誤訊息
針對資料來源中發生的錯誤，ODBC 驅動程式會傳回 ODBC 檔案程式庫傳回的錯誤訊息。 針對 ODBC 驅動程式或驅動程式管理員所發生的錯誤，驅動程式會根據與 SQLSTATE 相關聯的文字傳回錯誤訊息。  
  
 錯誤訊息的格式如下：  
  
```  
[vendor][ODBC-component][data-source]message-text  
```  
  
 括弧中的前置詞 ( [] ) 識別錯誤的位置。 當驅動程式管理員發生錯誤時，不會提供 *資料來源* 。 當資料來源中發生錯誤時，[*廠商*] 和 [*ODBC 元件*] 前置詞會識別從資料來源接收錯誤之 ODBC 元件的廠商和名稱。  
  
 下表顯示驅動程式管理員和驅動程式 ISAM 所傳回的錯誤訊息：  
  
|錯誤訊息|錯誤位置|  
|-------------------|--------------------|  
|微軟[ODBC 驅動程式管理員] *message-text*|驅動程式管理員 ( # A0) |  
|微軟[ODBC *驅動程式名稱*]*message-text*|驅動程式 ISAM (請參閱驅動程式 ISAMs) |
