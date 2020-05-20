---
title: 處理 Visual C++ 中的錯誤 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- errors [ADO], Visual C++
- Visual C++ error handling [ADO]
ms.assetid: b7576f07-020a-45f7-9e79-b5756f33f7ab
author: rothja
ms.author: jroth
ms.openlocfilehash: 1628522a6ef1c9498ea26e987070ee9f3a873d19
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758844"
---
# <a name="handling-errors-in-visual-c"></a>處理 Visual C++ 的錯誤
在 COM 中，大部分的作業會傳回 HRESULT 傳回碼，指出函數是否已順利完成。 #Import 指示詞會針對每個「原始」方法或屬性產生包裝函式程式碼，並檢查傳回的 HRESULT。 如果 HRESULT 指出失敗，包裝函式程式碼會呼叫 _com_issue_errorex （）並以 HRESULT 傳回碼做為引數，以擲回 COM 錯誤。 可以在**try-catch**區塊中攔截 COM 錯誤物件。 （為了提高效率，請攔截 _com_error 物件的參考）。  
  
 請記住，這些是 ADO 錯誤：這是因為 ADO 作業失敗所造成。 基礎提供者傳回的錯誤會在**連接**物件的**錯誤**集合中顯示為**錯誤**物件。  
  
 #Import 指示詞只會為 ADO 中所宣告的方法和屬性建立錯誤處理常式。 不過，您可以藉由撰寫自己的錯誤檢查宏或內嵌函式，來利用這個相同的錯誤處理機制。 如需範例，請參閱 Visual C++®延伸模組主題。
