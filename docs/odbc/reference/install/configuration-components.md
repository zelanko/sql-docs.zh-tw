---
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
ms.openlocfilehash: 37c2518c3b18423c804631780ee4a18bff29d88b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81289009"
---
# <a name="configuration-components"></a>設定元件
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 包含在 Windows 作業系統中。 您只應該在舊版 Windows 上明確安裝 ODBC。  
  
 資料來源是由安裝程式 DLL 所設定，接著會視需要呼叫驅動程式安裝 Dll 和轉譯器安裝程式 dll。 安裝程式 DLL 可以直接從 [控制台] 叫用，或由另一個程式（也稱為*管理程式*）載入和呼叫。 下圖顯示設定元件之間的關聯性。  
  
 ![組態元件間的關聯性](../../../odbc/reference/install/media/pr30.gif "pr30")  
  
 如需這些元件的詳細資訊，請參閱本節結尾的下列主題。  
  
-   [安裝程式](../../../odbc/reference/install/setup-program.md)  
  
-   [安裝程式 DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [驅動程式安裝程式 DLL](../../../odbc/reference/install/driver-setup-dll.md)  
  
## <a name="see-also"></a>另請參閱  
 [安裝元件](../../../odbc/reference/install/installation-components.md)
