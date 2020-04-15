---
title: 驅動程式設定 DLL |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], driver setup DLL
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: 49bab021-81fa-402e-b7a4-a5214f1fadc4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0a2878591c92fe0b2070a295d9dc622c245c17e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306419"
---
# <a name="driver-setup-dll"></a>驅動程式安裝程式 DLL
> [!NOTE]  
>  從 Windows XP 和 Windows 伺服器 2003 開始,ODBC 包含在 Windows 作業系統中。 您只應在早期版本的 Windows 上顯式安裝 ODBC。  
  
 驅動程式設定 DLL 包含**配置驅動程式**和**配置DSN**功能。 **ConfigDriver**執行特定於驅動程式的安裝任務,例如將特定於驅動程式的資訊輸入註冊表。 **配置DSN**維護有關註冊表中數據來源的特定於驅動程序的資訊。 有關這些功能的完整說明,請參閱設定[DLL API 參考](../../../odbc/reference/syntax/setup-dll-api-reference.md)。  
  
 **ConfigDSN**呼叫安裝程式 DLL 中的以下函數來維護註冊表中的資料來源資訊:  
  
-   **SQLwriteSntoini**. 新增資料來源。  
  
-   **SQLremoveSnfromini**。 刪除數據源。  
  
-   **SQLWrite 私有設定檔字串**。 在數據源規範子鍵下編寫特定於驅動程序的值。  
  
-   **SQLGet私人設定檔字串**。 從數據源規範子鍵讀取特定於驅動程序的值。  
  
-   **SQLGet 翻譯器**。 提示使用者輸入翻譯人員姓名和選項。 此函數在轉換器設定 DLL 中呼叫**設定器**。  
  
 驅動程式設定 DLL 由驅動程式開發人員編寫。 它可以是驅動程式 DLL 的一部分,也可以是單獨的 DLL。
