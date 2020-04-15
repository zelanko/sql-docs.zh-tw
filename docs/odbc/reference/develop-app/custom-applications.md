---
title: 自訂應用程式 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], custom applications
- custom applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: f28178d9-ecd6-4e8c-9644-9bb624999dcb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df00a748ee4d5e3a63b32c95449417a1057b58e1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305279"
---
# <a name="custom-applications"></a>自訂應用程式
自定義應用程式通常為幾個 DBMS 執行特定任務。 例如,應用程式可能從單個 DBMS 檢索數據並生成報告,或者它可能在多個 DBMS 之間傳輸數據。 這些應用程式的共同點是,這些 DBMS 在編寫應用程式之前是已知的,並且不太可能在應用程式的生命週期內更改。  
  
 因此,自定義應用程式只需要很少或根本沒有互操作性。 應用程式開發人員可以為每個 DBMS 選擇一個驅動程式,並直接向這些驅動程式編寫代碼。 應用程式可以安全地包含特定於驅動程式的代碼,以利用這些驅動程式的功能,甚至可能調用本機資料庫 API 以使用 ODBC 不支援的功能。  
  
 大多數自定義應用程式的主要互操作性問題是目標 DBMS 將來是否會發生變化。 如果是這樣,可以通過編寫更多的可互操作代碼來簡化此過程。 然而,這種DBMS的這種變化是罕見的,通常需要大量的工作。 因此,自定義應用程式的開發人員很少選擇以犧牲功能為代價來增加互操作性;他們通常選擇在更改 DBMS 時重新編碼該功能。
