---
title: 設定元件 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289009"
---
# <a name="configuration-components"></a>設定元件
> [!NOTE]  
>  從 Windows XP 和 Windows 伺服器 2003 開始,ODBC 包含在 Windows 作業系統中。 您只應在早期版本的 Windows 上顯式安裝 ODBC。  
  
 數據源由安裝程式 DLL 配置,後者反過來呼叫驅動程式設定 DLL 和轉換器根據需要設定 DLL。 安裝程式 DLL 直接從控制面板調用,或者由另一個程式(稱為*管理程式*)載入和調用。 下圖顯示了配置元件之間的關係。  
  
 ![組態元件間的關聯性](../../../odbc/reference/install/media/pr30.gif "pr30")  
  
 有關這些元件的詳細資訊,請參閱本節末尾的以下主題。  
  
-   [安裝程式](../../../odbc/reference/install/setup-program.md)  
  
-   [安裝程式 DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [驅動程式安裝程式 DLL](../../../odbc/reference/install/driver-setup-dll.md)  
  
## <a name="see-also"></a>另請參閱  
 [安裝元件](../../../odbc/reference/install/installation-components.md)
