---
title: 移除傳遞延伸模組 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- removing delivery extensions
- deleting delivery extensions
- delivery extensions [Reporting Services], removing
ms.assetid: dcb7caf2-d19a-4bc5-afb3-2b61ad11cac5
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5efe51d0c91a0321a17e539aeddbb26f0dc3a5fe
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56036247"
---
# <a name="removing-a-delivery-extension"></a>移除傳遞延伸模組
  若要移除 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 傳遞延伸模組，請從設定檔直接移除傳遞延伸模組的 **Extension** 項目。 移除組態資訊之後，傳遞延伸模組就無法再用於報表伺服器。  
  
 一旦從設定檔移除傳遞延伸模組的對應 **Extension** 項目，就不需要在報表伺服器中註冊。 報表伺服器會從傳遞延伸模組的清單移除項目，並停用任何使用該傳遞延伸模組的訂閱。 當移除傳遞延伸模組時，使用者就不能再選取它做為通知的方法。  
  
## <a name="see-also"></a>另請參閱  
 [實作傳遞延伸模組](implementing-a-delivery-extension.md)   
 [Reporting Services 延伸模組程式庫](../reporting-services-extension-library.md)  
  
  
