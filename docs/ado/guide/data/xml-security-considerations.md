---
description: XML 安全性考量
title: XML 安全性考慮 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML security in ADO
ms.assetid: fadbd38e-6e7b-4b81-96ea-85169c664374
author: rothja
ms.author: jroth
ms.openlocfilehash: 608ad67d531573d0124ea312252e6d30c289bf15
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978789"
---
# <a name="xml-security-considerations"></a>XML 安全性考量
在記錄集物件上的 ADO 儲存和開啟方法，不會被視為要在 Internet Explorer 中執行的安全作業。 因此，如果在以瀏覽器裝載的應用程式或控制項中執行的腳本程式碼中使用這些方法，則瀏覽器的安全性設定將會影響其行為。  
  
 Internet Explorer 5 在網際網路區域中預設會提供這類作業的安全性限制。 在該設定下，記錄集無法對用戶端上的本機檔案系統進行任何存取，或存取已下載頁面之伺服器網域以外的任何資料來源。 具體而言，在瀏覽器主控制項內執行時，只有當記錄集位於下載網頁的相同伺服器上時，才能將其儲存回檔案。 同樣地，您也可以從檔案中載入記錄集，只是該檔案位於下載頁面的相同伺服器上。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](./persisting-records-in-xml-format.md)