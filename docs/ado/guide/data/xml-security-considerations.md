---
title: XML 安全性考量 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- XML security in ADO
ms.assetid: fadbd38e-6e7b-4b81-96ea-85169c664374
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a963126f6b659fc13cae849f3a17e607daed1994
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="xml-security-considerations"></a>XML 安全性考量
ADO 儲存和開啟資料錄集物件上的方法不會視為安全 Internet Explorer 中執行的作業。 因此，如果在應用程式或控制項裝載於瀏覽器中執行指令碼中使用這些方法，瀏覽器的安全性設定會影響其行為。  
  
 Internet Explorer 5 會提供這類作業的安全性限制，預設會在網際網路區域。 根據該設定，資料錄集無法對用戶端上的本機檔案系統中的任何存取，或存取已從中下載網頁伺服器之網域外部的任何資料來源。 具體而言，當瀏覽器主機內執行，資料錄集可以儲存回至檔案才下載頁面的來源在相同伺服器上。 同樣地，您可以藉由從檔案載入該檔案位於相同的伺服器下載頁面的來源時，才開啟資料錄集。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
