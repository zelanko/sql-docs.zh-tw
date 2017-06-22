---
title: "移除傳遞延伸模組 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- removing delivery extensions
- deleting delivery extensions
- delivery extensions [Reporting Services], removing
ms.assetid: dcb7caf2-d19a-4bc5-afb3-2b61ad11cac5
caps.latest.revision: 31
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 81cadbc6eb9b176555b8d5dd5f63ac827e84d7f6
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="removing-a-delivery-extension"></a>移除傳遞延伸模組
  若要移除[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]傳遞延伸模組，只要移除**延伸**傳遞延伸模組組態檔中的項目。 移除組態資訊之後，傳遞延伸模組就無法再用於報表伺服器。  
  
 一旦傳遞延伸模組的對應**延伸**從組態檔移除元素，它不會再向報表伺服器。 報表伺服器會從傳遞延伸模組的清單移除項目，並停用任何使用該傳遞延伸模組的訂閱。 當移除傳遞延伸模組時，使用者就不能再選取它做為通知的方法。  
  
## <a name="see-also"></a>另請參閱  
 [實作傳遞延伸模組](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
