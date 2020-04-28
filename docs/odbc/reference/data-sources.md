---
title: 資料來源 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC]
- data sources [ODBC], about data sources
ms.assetid: 4ae44fa2-0b9b-4e19-ab45-c1dc93b68406
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b7e464963471b0cad41c5b93d50507d0fa9bf96
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306509"
---
# <a name="data-sources"></a>資料來源
*資料來源*就是資料的來源。 它可以是檔案、DBMS 上的特定資料庫，甚至是即時的資料摘要。 資料可能位於與程式相同的電腦上，或位於網路上某處的另一部電腦上。 例如，資料來源可能是在作業系統/2®作業系統上執行的 Oracle DBMS，由 Novell® Netware 存取;透過閘道存取的 IBM DB2 DBMS;伺服器目錄中的 Xbase 檔案集合;或本機 Microsoft® Access 資料庫檔案。  
  
 資料來源的目的是要收集存取資料所需的所有技術資訊（驅動程式名稱、網路位址、網路軟體等等），並將其隱藏在使用者的位置。 使用者應該能夠查看包含薪資、庫存和人員的清單、從清單中選擇 [薪資]，然後讓應用程式連接到薪資資料，而不需要知道薪資資料所在的位置或應用程式如何到達。  
  
 「*資料來源*」一詞不應該與類似的詞彙混淆。 在此手冊中， *DBMS*或*資料庫*是指資料庫程式或引擎。 在*桌面資料庫（* 專為在個人電腦上執行，且通常缺乏完整的 SQL 和交易支援）和*伺服器資料庫（* 設計成在用戶端/伺服器的情況下執行，並以獨立的資料庫引擎和豐富的 sql 和交易支援）來表示）之間，會有進一步的區別。 *資料庫*也會參考特定的資料集合，例如目錄中的 Xbase 檔案集合或 SQL Server 上的資料庫。 這通常等同于在此手冊中的其他地方使用的「*目錄*」一詞，或舊版 ODBC 中的「詞彙辨識*符號*」。  
  
 此章節包含下列主題。  
  
-   [資料來源的類型](../../odbc/reference/types-of-data-sources.md)  
  
-   [使用資料來源](../../odbc/reference/using-data-sources.md)  
  
-   [資料來源範例](../../odbc/reference/data-source-example.md)
