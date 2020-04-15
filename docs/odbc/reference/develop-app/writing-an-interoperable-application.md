---
title: 編寫可互通的應用程式 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289080"
---
# <a name="writing-an-interoperable-application"></a>撰寫可互通的應用程式
每當應用程式對多個驅動程式使用相同的代碼時,該代碼必須在這些驅動程序之間互通。 在大多數情況下,這是一個簡單的任務。 例如,對於所有驅動程式,使用僅轉發游標獲取行的代碼都相同。 在某些情況下,這可能更加困難。 例如,建構用於 SQL 語句的標識符的代碼需要考慮標識符大小寫、報價以及一部分、兩部分和三部分命名約定。  
  
 通常,可互操作的代碼必須處理功能支援和功能可變性問題。 *功能支援*是指是否支援特定功能。 例如,並非所有 DBMS 都支援事務,並且無論事務支援如何,可互通的代碼都必須正常工作。 *特徵可變性*是指支援特定要素的方式變化。 例如,目錄名稱放置在某些 DBMS 中的標識符開頭,並在其他 DBM 的標識符末尾放置。  
  
 應用程式可以在設計時或運行時處理功能支援和功能可變性。 為了在設計時處理功能支援和可變性,開發人員查看目標 DBMS 和驅動程式,並確保相同的代碼在它們之間可互通。 這通常是低或有限互操作性的應用程式處理這些問題的方式。  
  
 例如,如果開發人員保證垂直應用程式僅使用四個特定的 DBMS,並且如果每個 DBMS 都支援事務,則應用程式不需要代碼來檢查運行時的事務支援。 它始終可以假定事務可用,因為設計時決定僅使用四個 DBMS,每個 DBMS 都支援事務。  
  
 為了在運行時處理功能支援和可變性,應用程式必須在運行時測試不同的功能並相應地執行操作。 這通常是高度可互操作的應用程式處理這些問題的方式。 對於功能支援問題,這意味著編寫使要素可選的代碼或編寫在功能不可用時類比該功能的代碼。 對於功能可變性問題,這意味著編寫支援所有可能變體的代碼。  
  
 此章節包含下列主題。  
  
-   [檢查功能支援和變化性](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [要監看的功能](../../../odbc/reference/develop-app/features-to-watch-for.md)
