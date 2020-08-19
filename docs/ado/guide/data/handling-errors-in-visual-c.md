---
description: 處理 Visual C++ 的錯誤
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
ms.openlocfilehash: 4b43b8314e47c8a96dadcf8cab841a37da0c0518
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453290"
---
# <a name="handling-errors-in-visual-c"></a>處理 Visual C++ 的錯誤
在 COM 中，大部分的作業會傳回 HRESULT 傳回碼，指出函式是否已順利完成。 #Import 指示詞會針對每個「原始」方法或屬性來產生包裝函式程式碼，並檢查傳回的 HRESULT。 如果 HRESULT 指出失敗，包裝函式程式碼會藉由以 HRESULT 傳回碼作為引數來呼叫 _com_issue_errorex ( # A1 來擲回 COM 錯誤。 COM 錯誤物件可以在 **try-catch** 區塊中捕捉。  (為了提高效率，請攔截 _com_error 物件的參考。 )   
  
 請記住，這些是 ADO 錯誤：由於 ADO 作業失敗所造成。 基礎提供者所傳回的錯誤會在**連接**物件的**錯誤**集合中顯示為**錯誤**物件。  
  
 #Import 指示詞只會針對在 ADO 中宣告的方法和屬性建立錯誤處理常式。 不過，您可以藉由撰寫自己的錯誤檢查宏或內嵌函式，來利用這個相同的錯誤處理機制。 如需範例，請參閱 Visual C++®擴充功能主題。
