---
title: 保留字 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- reserved words [Master Data Services]
- Master Data Services, reserved words
ms.assetid: 88afd0d0-4362-4394-8357-4e65388fc0fc
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: cd1e5bcee01992607cf9bffca1a72dd99bd75fbe
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84960578"
---
# <a name="reserved-words-master-data-services"></a>保留字 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，當您建立模型物件或成員時，無法使用某些字詞。 使用這些字詞可能會導致錯誤。  
  
> [!NOTE]  
>  您也應該對使用特殊字元 (符號、連字號等) 加以限制。  
  
-   [模型](#models)  
  
-   [實體](#entities)  
  
-   [明確階層](#exhierarchies)  
  
-   [屬性](#attributes)  
  
-   [屬於](#members)  
  
##  <a name="models"></a><a name="models"></a>機型  
 如果您建立一個名稱設定為 **Name**的模型，請勿選取 **[建立與模型同名的實體]** ，因為 **Name** 無法用於實體的名稱。  
  
##  <a name="entities"></a><a name="entities"></a>條目  
 您無法針對實體名稱使用 **Name** 或 **Code**。  
  
##  <a name="explicit-hierarchies"></a><a name="exhierarchies"></a>明確階層  
 您無法針對明確階層名稱使用 **Name** 或 **Code**。  
  
##  <a name="attributes"></a><a name="attributes"></a>特性  
  
-   **識別碼**  
  
-   **程式碼**  
  
-   **名稱**  
  
-   **EnterDTM**  
  
-   **EnterUserID**  
  
-   **EnterUserName**  
  
-   **LastChgDTM**  
  
-   **LastChgUserID**  
  
-   **Status_ID**  
  
-   **ValidationStatus_ID**  
  
-   **Version_ID**  
  
##  <a name="members"></a><a name="members"></a>屬於  
 對於成員而言，您無法針對 **[Code]** 屬性值使用 **MDMMemberStatus** 或 **ROOT** 。  
  
## <a name="see-also"></a>另請參閱  
 [Master Data Services 概觀](master-data-services-overview-mds.md)  
  
  
