---
title: XML 安全性考量 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML security in ADO
ms.assetid: fadbd38e-6e7b-4b81-96ea-85169c664374
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8e5ef2215725382650540d24f90e7cbd61102a71
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704429"
---
# <a name="xml-security-considerations"></a>XML 安全性考量
ADO 儲存及開啟資料錄集物件上的方法較不安全的作業，在 Internet Explorer 中執行。 因此，如果在應用程式或控制項裝載於瀏覽器中執行指令碼中使用這些方法，則瀏覽器的安全性組態會有影響其行為。  
  
 Internet Explorer 5 預設網際網路區域中提供這類作業的安全性的限制。 根據該設定，無法對用戶端上的本機檔案系統中的任何存取資料錄集，或將其存取從中下載網頁伺服器之網域以外的任何資料來源中。 具體來說，當瀏覽器主機內執行，資料錄集可以儲存回到檔案相同的伺服器，從中下載頁面上才。 同樣地，您也可以藉由從檔案載入該檔案位於相同的伺服器，從中下載頁面時，才開啟資料錄集。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
