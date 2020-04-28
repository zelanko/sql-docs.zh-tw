---
title: XML 安全性考慮 |Microsoft Docs
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
ms.openlocfilehash: fa0e9e2df1e8ba3f44b10e662d25e536ac7962f8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923352"
---
# <a name="xml-security-considerations"></a>XML 安全性考量
在「記錄集」物件上的 ADO Save 和 Open 方法不會被視為在 Internet Explorer 中執行的安全作業。 因此，如果這些方法用於在瀏覽器中裝載的應用程式或控制項中執行的腳本，則瀏覽器的安全性設定將會影響其行為。  
  
 Internet Explorer 5 預設會在網際網路區域中提供這類作業的安全性限制。 在該設定之下，記錄集無法對用戶端上的本機檔案系統進行任何存取，或存取已下載頁面之伺服器網域以外的任何資料來源。 具體而言，在瀏覽器主控制項內執行時，只有當記錄集位於頁面下載所在的同一部伺服器上時，才可以將它儲存回檔案。 同樣地，您也可以從檔案載入記錄集，只在該檔案位於已下載頁面的相同伺服器上時才會開啟。  
  
## <a name="see-also"></a>另請參閱  
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
