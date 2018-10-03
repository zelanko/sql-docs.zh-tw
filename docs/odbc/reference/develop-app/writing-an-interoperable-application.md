---
title: 撰寫可互通的應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: 8b42b8ae-7862-4b63-a0b3-2a204e0c43a5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8e559eab5787a64b6bdf0850147d7d9128fc435c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47757256"
---
# <a name="writing-an-interoperable-application"></a>撰寫可互通的應用程式
每當應用程式使用相同的程式碼對多個驅動程式，該程式碼必須在這些驅動程式之間的互通性。 在大部分情況下，這是件簡單的工作。 比方說，程式碼來擷取順向資料指標的資料列也適用於所有的驅動程式。 在某些情況下，這可以是更困難。 比方說，建構 SQL 陳述式中使用的識別項的程式碼必須考慮識別碼大小寫、 加註引號於，以及一段、 兩部分和三部分命名慣例。  
  
 一般情況下，互通性的程式碼必須處理所支援之功能和功能的變化性的問題。 *功能支援*是指是否支援特定功能。 比方說，並非所有的 Dbms 支援交易，並可互通的程式碼必須正確運作，不論交易支援。 *功能的變化性*指的是受到特定功能的方式中的變異。 比方說，目錄名稱會放在某些 Dbms 中的識別項的開頭和結尾的其他項目中的識別項。  
  
 在設計階段或執行階段，應用程式可以處理所支援之功能與功能的變化性。 若要在設計階段處理功能的支援和變化，開發人員會查看目標 Dbms 和驅動程式，並可確保相同的程式碼將會在它們之間的互通性。 這通常是在其中具有低或只有有限的互通性的應用程式處理這些問題的方式。  
  
 例如，如果開發人員可保證，垂直應用程式只會使用四個特定的 Dbms，而且每個這些 Dbms 支援交易，應用程式不會不會需要程式碼，以檢查在執行階段的交易支援。 它永遠可以假設交易可因為設計階段決定来使用只有四個 Dbms，其中每個支援交易。  
  
 若要在執行階段處理功能的支援和變化，應用程式必須在執行階段測試不同的功能，並採取適當動作。 這通常是在其中高度互通的應用程式需要處理這些問題的方式。 功能的支援問題，這表示撰寫程式碼，可讓無法使用時，模擬此功能的功能選擇性或撰寫程式碼。 對於功能變化性的問題，這表示撰寫支援所有可能變化的程式碼。  
  
 此章節包含下列主題。  
  
-   [檢查功能支援和變化性](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [功能](../../../odbc/reference/develop-app/features-to-watch-for.md)
