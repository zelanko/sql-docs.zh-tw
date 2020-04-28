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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 553e718e0759e47701e7f8c04561693358d5dc52
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81289080"
---
# <a name="writing-an-interoperable-application"></a>撰寫可互通的應用程式
每當應用程式對一個以上的驅動程式使用相同的程式碼時，該程式碼必須可在這些驅動程式之間互通。 在大部分的情況下，這是很簡單的工作。 例如，以順向資料指標提取資料列的程式碼，對所有驅動程式而言都是相同的。 在某些情況下，這可能會比較棘手。 例如，要在 SQL 語句中用來建立識別碼的程式碼，必須考慮使用識別碼大小寫、加上引號和一部分、兩部分和三部分命名慣例。  
  
 一般來說，互通程式碼必須處理功能支援和功能變異的問題。 *功能支援*是指是否支援特定功能。 例如，並非所有 Dbms 都支援交易，而不論交易支援為何，互通程式碼都必須正確運作。 *功能*變異指的是支援特定功能的方式變化。 例如，類別目錄名稱會放在某些 Dbms 中的識別碼開頭，以及其他人的識別碼結尾。  
  
 應用程式可以在設計階段或執行時間處理功能支援和功能的變異。 為了在設計階段處理功能支援和變化，開發人員會查看目標 Dbms 和驅動程式，並確保相同的程式碼可在兩者間互通。 這通常是具有低或有限互通性的應用程式處理這些問題的方式。  
  
 例如，如果開發人員保證垂直應用程式只會使用四個特定的 Dbms，而且如果每一個 Dbms 都支援交易，應用程式就不需要在執行時間檢查交易支援的程式碼。 因為設計階段決策只會使用四個 Dbms，而每個都支援交易，所以它一定會假設有可用的交易。  
  
 若要在執行時間處理功能支援和變化性，應用程式必須在執行時間測試不同的功能，並據以採取行動。 這通常是可高度互通的應用程式處理這些問題的方式。 針對功能支援問題，這表示撰寫程式碼，使功能在無法使用時可選擇或撰寫模擬功能的程式碼。 對於功能變異問題，這表示撰寫支援所有可能變化的程式碼。  
  
 此章節包含下列主題。  
  
-   [檢查功能支援和變化性](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [要監看的功能](../../../odbc/reference/develop-app/features-to-watch-for.md)
