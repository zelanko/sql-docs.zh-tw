---
description: 設定元件
title: 設定元件 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], configuring
ms.assetid: 0b68ff48-12e4-41aa-b9e2-b39ed5023ea7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a8a4b0f0b0a7a99409b5bb9caea53f23b62457e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487431"
---
# <a name="configuration-components"></a>設定元件
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 會包含在 Windows 作業系統中。 您應該只在舊版的 Windows 上明確地安裝 ODBC。  
  
 資料來源是由安裝程式 DLL 設定，接著會依需要呼叫驅動程式安裝 Dll 和轉譯程式安裝 Dll。 安裝程式 DLL 可直接從主控台叫用，也可以由另一個程式（稱為 *管理程式*）載入和呼叫。 下圖顯示設定元件之間的關聯性。  
  
 ![組態元件間的關聯性](../../../odbc/reference/install/media/pr30.gif "pr30")  
  
 如需這些元件的詳細資訊，請參閱本節結尾的下列主題。  
  
-   [安裝程式](../../../odbc/reference/install/setup-program.md)  
  
-   [安裝程式 DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [驅動程式安裝程式 DLL](../../../odbc/reference/install/driver-setup-dll.md)  
  
## <a name="see-also"></a>另請參閱  
 [安裝元件](../../../odbc/reference/install/installation-components.md)
