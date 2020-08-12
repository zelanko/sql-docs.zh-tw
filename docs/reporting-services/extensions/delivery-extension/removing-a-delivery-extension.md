---
title: 移除傳遞延伸模組 | Microsoft Docs
description: 了解如何從 Reporting Services 移除傳遞延伸模組，讓報表伺服器不會將其列為可用，並停用使用該項目的訂閱。
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- removing delivery extensions
- deleting delivery extensions
- delivery extensions [Reporting Services], removing
ms.assetid: dcb7caf2-d19a-4bc5-afb3-2b61ad11cac5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6f4f23d58836dbadb9393be49dd34425c89a15c3
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529484"
---
# <a name="removing-a-delivery-extension"></a>移除傳遞延伸模組
  若要移除 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 傳遞延伸模組，請從設定檔直接移除傳遞延伸模組的 **Extension** 項目。 移除組態資訊之後，傳遞延伸模組就無法再用於報表伺服器。  
  
 一旦從設定檔移除傳遞延伸模組的對應 **Extension** 項目，就不需要在報表伺服器中註冊。 報表伺服器會從傳遞延伸模組的清單移除項目，並停用任何使用該傳遞延伸模組的訂閱。 當移除傳遞延伸模組時，使用者就不能再選取它做為通知的方法。  
  
## <a name="see-also"></a>另請參閱  
 [實作傳遞延伸模組](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
