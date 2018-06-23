---
title: 保留字 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- reserved words [Master Data Services]
- Master Data Services, reserved words
ms.assetid: 88afd0d0-4362-4394-8357-4e65388fc0fc
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 3307fb8185abfb6b862e72691596e4385b09dcb8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145876"
---
# <a name="reserved-words-master-data-services"></a>保留字 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，當您建立模型物件或成員時，無法使用某些字詞。 使用這些字詞可能會導致錯誤。  
  
> [!NOTE]  
>  您也應該對使用特殊字元 (符號、連字號等) 加以限制。  
  
-   [模型](#models)  
  
-   [實體](#entities)  
  
-   [明確階層](#exhierarchies)  
  
-   [屬性](#attributes)  
  
-   [成員](#members)  
  
##  <a name="models"></a> 模型  
 如果您建立一個名稱設定為 **Name**的模型，請勿選取 **[建立與模型同名的實體]** ，因為 **Name** 無法用於實體的名稱。  
  
##  <a name="entities"></a> 實體  
 您無法針對實體名稱使用 **Name** 或 **Code**。  
  
##  <a name="exhierarchies"></a> 明確階層  
 您無法針對明確階層名稱使用 **Name** 或 **Code**。  
  
##  <a name="attributes"></a> 屬性  
  
-   **ID**  
  
-   **[字碼]**  
  
-   **名稱**  
  
-   **EnterDTM**  
  
-   **EnterUserID**  
  
-   **EnterUserName**  
  
-   **LastChgDTM**  
  
-   **LastChgUserID**  
  
-   **Status_ID**  
  
-   **ValidationStatus_ID**  
  
-   **Version_ID**  
  
##  <a name="members"></a> 成員  
 對於成員而言，您無法針對 **[Code]** 屬性值使用 **MDMMemberStatus** 或 **ROOT** 。  
  
## <a name="see-also"></a>另請參閱  
 [Master Data Services 概觀](master-data-services-overview-mds.md)  
  
  