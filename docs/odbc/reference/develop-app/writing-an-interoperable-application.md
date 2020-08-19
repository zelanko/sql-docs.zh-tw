---
description: 撰寫可互通的應用程式
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
ms.openlocfilehash: 0d8bff1848e20705ab64b8284ed42331c80fb23a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421362"
---
# <a name="writing-an-interoperable-application"></a>撰寫可互通的應用程式
每當應用程式對一個以上的驅動程式使用相同的程式碼時，該程式碼必須可在這些驅動程式之間互通。 在大部分的情況下，這是一項簡單的工作。 例如，使用順向資料指標提取資料列的程式碼對所有驅動程式都是相同的。 在某些情況下，這可能更困難。 例如，用來建立 SQL 語句中所使用之識別碼的程式碼，必須考慮識別碼大小寫、引號和一部分、兩部分和三部分命名慣例。  
  
 一般而言，可互通的程式碼必須處理功能支援和功能變化的問題。 *功能支援* 是指是否支援特定功能。 例如，並非所有 Dbms 都支援交易，而不論交易支援為何，可互通的程式碼都必須正常運作。 *特性* 變異指的是支援特定功能的方式。 例如，目錄名稱會放在部分 Dbms 的識別碼開頭，以及其他 Dbms 的識別碼結尾。  
  
 應用程式可以在設計階段或執行時間處理功能支援和功能變化。 為了在設計階段處理功能支援和變化，開發人員會探討目標 Dbms 和驅動程式，並確定相同的程式碼在兩者之間都能互通。 這通常是指具有低或受限互通性的應用程式處理這些問題的方式。  
  
 例如，如果開發人員保證垂直應用程式只能搭配四個特定的 Dbms 運作，而且如果這些 Dbms 都支援交易，則應用程式不需要程式碼就能在執行時間檢查交易支援。 它一律會假設交易可供使用，因為設計階段決定只使用四個 Dbms，每一個 Dbms 都支援交易。  
  
 若要在執行時間處理功能支援和變化性，應用程式必須在執行時間測試不同的功能，並據此採取行動。 這通常是高度互通的應用程式處理這些問題的方式。 針對功能支援問題，這表示撰寫程式碼，讓功能成為選擇性或撰寫程式碼，以在無法使用時模擬功能。 針對功能變異問題，這表示撰寫支援所有可能變異的程式碼。  
  
 此章節包含下列主題。  
  
-   [檢查功能支援和變化性](../../../odbc/reference/develop-app/checking-feature-support-and-variability.md)  
  
-   [要監看的功能](../../../odbc/reference/develop-app/features-to-watch-for.md)
